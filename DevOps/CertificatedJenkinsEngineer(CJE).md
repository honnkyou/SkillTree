## Certificated Jenkins Engineer(CJE)
### Register for exam
- [Link](https://www.webassessor.com/wa.do?page=enterCatalog&branding=CLOUDBEES&tabs=111)
- 费用: 150$

### Install Jenkins
- Docker
```bash
# docker pull jenkins/jenkins:lts
# mkdir /mydata/jenkins_home
# chown -R 1000:1000 /mydata/jenkins_home // the UID of jenkins is 1000
# docker run -di --name=jenkins -p 8080:8080 -v /mydata/jenkins_home/:/var/jenkins_home jenkins/jenkins:lts
```

- Local VM: Vagrant + Virtualbox
	- for Jenkins Administration
		- [DownLoad Zip file](https://s3.amazonaws.com/cloudbees-training-materials/training-admin-fundamentals/master/cloudbees-training-admin-fundamentals.zip)
		- Start VM
		```
        //1. unzip the file
        //2. cd <path of training-admin-fundamentals/>
        //3. confirm Vagrantfile
        # ls -l Vagrantfile
        //4. start VM
        # vagrant up 
        ```
	- for Jenkins Pipeline
		- [DownLoad Zip file](https://s3.amazonaws.com/cloudbees-training-materials/training-pipeline-fundamentals/master/cloudbees-training-pipeline-fundamentals.zip)
		- Start VM
		```
        //1. unzip the file
        //2. cd <path of training-pipeline-fundamentals/>
        //3. confirm Vagrantfile
        # ls -l Vagrantfile
        //4. start VM
        # vagrant up 
        ```
- OS native packages(Yum)
- WAR

### Reference Sources
#### 1. CloudBees University
- [Jenkins - Fundamentals](https://standard.cbu.cloudbees.com/cloudbees-university-jenkins-fundamentals) 
- [Jenkins Administration - Fundamentals](https://standard.cbu.cloudbees.com/cloudbees-university-jenkins-administration-fundamentals)
- [Jenkins Pipeline - Fundamentals](
https://standard.cbu.cloudbees.com/cloudbees-university-jenkins-pipeline-fundamentals)
#### 2. jenkins.io/documentation
- [Using Jenkins](jenkins.io/doc/book/using/)
- [Managing Jenkins](https://www.jenkins.io/doc/book/managing/)
- [System administration Jenkins](https://www.jenkins.io/doc/book/system-administration/)
#### 3. searched from GitHub
- [dingliu/Certified Jenkins Engineer (CJE) Exam Study Notes](https://github.com/dingliu/Certified-Jenkins-Engineer-Study-Notes)
- [harikak84/Certified-Jenkins-Engineer(Linux Academy)](https://github.com/harikak84/Certified-Jenkins-Engineer)
- [m0un10/Jenkins Certified Engineer (JCE)](https://github.com/m0un10/jenkins-certified-engineer)
- [luckylittle/Certified Jenkins Engineer (CJE Note) 2017](https://github.com/luckylittle/jenkins-ci)
- [bmuschko/Certified Jenkins Engineer (CJE) Prep Course](https://github.com/bmuschko/cje-prep)
- [melmols/Certified-Jenkins-Engineer-CJE](https://github.com/melmols/Certified_Jenkins_Engineer_CJE)
- [jenkins-zh/Jenkins系列教程](https://github.com/jenkins-zh/jenkins-zh/issues/345)

#### (optional)Blog for how to prepare CJE
- [Preparation Guide for the Certified Jenkins Engineer Exam](https://www.whizlabs.com/blog/certified-jenkins-engineer-exam-preparation/)
- [Blog from deng for preparing for CJE exam](https://ottodeng.io/post/cje/)
- [我获得了Certified Jenkins Engineer认证及证书](https://www.shanyshanb.com/post/i-get-certified-jenkins-engineer-credential)
