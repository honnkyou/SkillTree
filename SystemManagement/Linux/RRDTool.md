# 1. RRDTool简介
- [官方教程](http://oss.oetiker.ch/rrdtool/doc/index.en.html)
- [ade兄的大作](http://bbs.chinaunix.net/thread-552220-1-1.html)
- [alims兄的RRDtool简体中文教程 v1.01](http://bbs.chinaunix.net/thread-2150417-1-1.html)

 RRDTool是用于绘制资源，流量变化等的工具。其前身是名为MRTG的工具。MRTG是一款很容易就可以绘制出资料流量等统计图表的工具，尤其是还提供了自动生成配置文件的 cfgmaker 和自动生成 HTML 页面的 indexmaker 这两个工具，让你省去逐个编写 cfg 文件的痛苦。
 不过在使用MRTG中却常遇到一下几个问题：
 1. MRTG 一张图表只能显示2个对象，一个输入，一个输出。如果你想同时显示多个对象呢？只能绘制多张图表。
 2. MRTG无法回放数据。MRTG 的图是自动生成的，所采用的数据也是由 MRTG 自己提取的,合并后的数据无法回放为原来数据。
 3. MRTG 只有 COUNTER 和 GAUGE 这两种计算类新。且对负数或'.15'类的小数识别会出错。
 4. MRTG 无法实现有条件的绘图。只绘制出某种类型的有条件图表无法实现。

RRDTool 绘制图表流程如下。
```
 数据的采集→插入数据→提取数据→绘图→建立 HTML
```
## 1.1 RRDTool的定义
 [RRDTool](http://oss.oetiker.ch/rrdtool/)是"Round Robin Database tool"的缩写，作者同时也是MRTG的发明人。 所谓的“Round Robin” 其实是一种存储数据的方式，使用`固定大小`的空间来存储数据，并有一个指针指向最新的数据的位置。
我们可以把用于存储数据的数据库的空间看成一个`圆`，上面有很多刻度。这些刻度所在的位置就代表用于存储数据的地方。
所谓指针，可以认为是从圆心指向这些刻度的一条直线。指针会随着数据的读写操作绕着圆心自动移动。因为圆无所谓起点与终点，所有指针可以一直绕圆心移动，当所有的空间都存满了数据，就又从头开始存放。
因为可以视其为圆形结构，所有整个存储空间的大小就是一个固定的数值。
RRDtool 所使用的数据库文件的后缀名是`.rrd`。
## 1.2 RRDTool的特殊处
 1. RRDTool扮演两个角色，从可以存储角度RRDTool可以视为后台数据库的一种；同时RRDTool又允许创建图表，又可以视为前台绘制工具。
 2. RRDTool的每个rrd文件的大小固定不变。普通数据库文件随时间增大。
 3. 其他数据块只能被动接受数据，RRDTool可以对接受的数据进行计算。例如前后两个数据的变化程度（rate of  change），并存储该结果。
 4. RRDtool 要求定时获取数据，其他数据库则没有该要求。如果在一个时间间隔内（heartbeat）没有收到值，则会用 UNKN 代替。

# 2. 安装
## 2.1 RHEL 系
 RHEL系最简单的安装方式就是用Yum在线安装。
```shell
  # yum install rrdtool -y
```
 成功安装完后可通过下面命令确认，并查看有无rrdtool命令。

```shell
# rpm -qa | grep rrdtool
```

# 3. 前期规划
 俗话说：磨刀不误砍柴工。好的规划必须具备灵活性、可扩展性，否则会给将来的使用带来不少的麻烦。

## 3.1 RRDTool的前期规划
 1. `一个RRD文件中规划多少个监视对象(DS)`RRDtool 提供了 tune 操作，可以增加或着删除RRD文件中的某个对象，而且绘图是也可以指定要绘制哪个对象的图。
 2. `取样频率的规划`可以是5分钟，20分钟，2小时，1天等。
 3. `如何保存/统计数据：`RRDTool的数据存放需要自己定义。可以参照MRTG的方式。
  * 每日统计图（5分钟平均）  ： 600 个，大约2天的时间
  * 每周统计图（20分钟平均） ： 600 个，大约8天的时间
  * 每月统计图 （2小时平均） ： 600 个，50 天的时间
  * 每年统计图 （1天平均） ：730 个， 2年的时间
 4. `以什么方式绘图：`绘图方式有`曲线(LINE)``方块(AREA)``STACK`，STACK方式是在前一个的基础上绘制图形。

## 3.2 规划实例
 1. `搞清楚究竟想要监测什么对象 ：`检测本地主机的网络流量。包括eth0,lo接口。
 2. `想要以什么方法来取得数据 ：`sar也可以统计网卡接口的流量，这里列出使用python和snmp的方式。
 3. `取样频率：`5分钟
 4. `RRD文件数量：`2个RRD文件，eth0.rrd和lo.rrd
 5. `为检测对象命名：`eth0_in;eth0_out;lo_in;lo_out
 6. `统计频率：`5分钟600个样本(每日)；20分钟600个样本(每周)；2小时600个样本(每月)；1天730个样本(每年)
 7. `以什么方式绘图：`待定。 

