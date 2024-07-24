---
title: "Project Guide On Jenkins Integration with Sonar Server: A Complete Guide"
seoTitle: "Jenkins and Sonar Server Integration Guide"
seoDescription: "A comprehensive guide to integrating Jenkins with SonarQube to enhance code quality, automate checks, and improve software development efficiency"
datePublished: Wed Jul 24 2024 10:29:40 GMT+0000 (Coordinated Universal Time)
cuid: clyzpdh8y000c09i4ggtl4t5a
slug: project-guide-on-jenkins-integration-with-sonar-server-a-complete-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721808458989/d3b45134-88ac-4e7b-bf9e-e919c72073c9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721816933544/a12af03a-5917-4d32-ab31-a887c4563e0e.png
tags: projects, sonarqube, devops, jenkins, tws, diu

---

**Enhancing Code Quality with Jenkins Integration and Sonar Server 🚀**

In today's fast-paced software development world, ensuring high code quality is crucial. 🌟 One powerful way to achieve this is by integrating Jenkins with Sonar Server. Let's dive into how this dynamic duo can supercharge your development process! 💻

### Why Sonar Server?

[**Sonar Server**](https://www.sonarqube.org/) (or **SonarQube** ) is an open-source platform for continuous inspection of code quality. It performs automatic reviews with static analysis of code to detect bugs, code smells, and security vulnerabilities.

### What is Jenkins?

[Jenkins](https://www.jenkins.io/) is an open-source automation server that helps automate the building, testing, and deployment of applications. It's incredibly flexible and extensible, making it a favorite among developers for continuous integration and delivery (CI/CD).

### Benefits of Integration

⚙️ **Automated Code Quality Checks:** Jenkins can trigger SonarQube scans automatically whenever code is pushed or merged, ensuring every change undergoes rigorous quality checks.

📈 **Centralized Reporting:** SonarQube provides detailed reports on code quality metrics, such as code coverage, duplications, and complexity. Integration with Jenkins makes these reports easily accessible to the entire team.

🔒 **Early Detection of Issues:** By integrating SonarQube into your Jenkins pipeline, potential issues like bugs or security vulnerabilities are caught early in the development cycle, reducing the cost and effort of fixing them later.

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721809859283/9c1cd0ed-e630-41b5-9789-f8cf4573d53b.jpeg align="center")

### Setting Up Jenkins and Sonar Server

**On AWS EC2 Machine Deploy Jenkins Server**

### Prerequisite (Step 1 )

* Jenkins installation on AWS EC2
    
* Create an EC2 instance with ubuntu Linux AMI
    
* Connect to your EC2 instance
    
* Update all packages by following command :
    
* ```bash
          $sudo apt update -y
    ```
    
* Install java by following command :
    
* ```bash
        sudo apt install openjdk-11-jdk -y
    ```
    
    ### Step 2
    
    Jenkins installation on AWS EC2 Using apt
    
    Add Jenkins to your apt Repository using following command
    
* ```bash
      sudo wget -q -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
      echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
      sudo apt-get update
      sudo apt-get install jenkins
    ```
    
    Start and Enable Jenkins Service
    

```bash
$sudo systemctl start Jenkins
$sudo systemctl enable jenkins
$sudo systemctl status jenkins
```

Get the initial administration password

```bash
$sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### step 3

Open your EC2 instance public IP (https://&lt;public\_IP&gt;:8080/) along with port 8080 in your favorite browser. And provide the administration password obtained during the installation.

> Note: Make sure you enable 8080 port in Security Group Inbound Rules.

Provided password which we have copied to unlock Jenkins.

Select "Install Suggested Plugins" Card (It will install those plugins )

**Here is your Jenkins server all set**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720176148435/7053e99f-af62-4c7c-9daa-e59ebb0955d9.jpeg align="center")

**<mark>On AWS EC2 Machine Deploy SonarQube Server</mark>**

### Environment Setup🖥️

**<mark>Pre-requites:</mark>**

Java is installed on your Machine

if SonarQube 7.6 ----&gt; Java 1.8 version is installed

if SonarQube 7.6 -----&gt; java 11 version is Installed

> Note : We can Check this Compatability in official SonarQube Website

**Hardware Requirements**

Minimum RAM : 2 GB

### ⚙️Step for deploy SonarQube

Create EC2 Instance with 4 GB Ram (t2.medium )

Connect with EC2 instance using Git-Bash

Switch to Root User

```bash
sudo -i
```

Update packages

```bash
sudo apt update -y
```

Install wget package using following command

```bash
sudo apt install wget -y
```

change directory

```bash
cd /opt
```

```bash
sudo apt install openjdk-11-jdk -y
java -versionInstall java openjdk
```

unzip package install

```bash
sudo apt install unzip -y
```

install SonarQube zip file change version according to your version

```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.4.0.35506.zip
```

unzip file

```bash
unzip sonarqube-8.4.0.35506.zip
```

> Note : SonarQube Server Will Not Run With Root User
> 
> we have to create new user called Sonar

create new user

```bash
useradd sonar
```

```bash
visudo
```

File be look like below image we have to configure user n passwd

**sonar ALL=(ALL) NOPASSWD: ALL**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721322222601/34458457-9169-4663-9a3e-e0afb62bc578.jpeg align="center")

change Ownership for Sonar Folder

```bash
chown -R sonar:sonar /opt/sonarqube-8.4.0.35506
```

Change file permission

```bash
chmod -R 775 /opt/sonarqube-8.4.0.35506
```

Now switch to Sonar user

```bash
su - sonar
```

Go to SonarQube folder

```bash
cd sonarqube-8.4.0.35506
```

```bash
cd bin
```

```bash
cd linux-x86-64
```

```bash
./sonar.sh start
```

**<mark>Congratulations to yourself!</mark>**

**Access your SonarQube :**

URL : http : // EC2-VM-Public-IP :9000/

> Note : SonarQube runs on 9000 port by Default . Enable this port in security group as custom TCP

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721394003328/17d97eb6-8557-4821-b103-98a6687b2589.jpeg align="center")

---

### Now Sonar Server With Jenkins Integration

### Pre - Requisites

1. SonarQube Server (already we done that using above steps )
    
2. Jenkins Server (already we done that using above steps )
    
3. On SonarQube Server generate a Token
    

**Steps configure Token**

Go to Sonar ---&gt;Login ---&gt; Click On profile ----&gt; My Account ---&gt; Security ---------------&gt;Generate Token

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721405799926/3f97af35-cad4-43a5-98ac-8efd43c86f57.jpeg align="center")

4. On Jenkins Server
    

* Install Apache maven
    
* Install Sonar Plugins
    
* Configure SonarQube Credentials
    
* Install Sonar Scanner
    
* Run Jenkins Pipeline Job
    

Execute Below Commands In Jenkins Server VM CLI

```bash
sudo su
```

```bash
cd /opt
```

```bash
wget https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz
```

```bash
tar -xvf apache-maven-3.8.8-bin.tar.gz
```

**<mark>Now go to Jenkins Dashboard</mark>**

**Install Scanner Plugin**

* Click on Manage Jenkins
    
* Click on Plugins then go to Available
    
* Click On SonarQube Scanner Plugin
    
* Install It
    

**Configure SonarQube Server**

* Click on Manage Jenkins
    
* click on configure System
    
* Go to SonarQube Server
    
* Add SonarQube Server
    

> Name: Sonar -server -7.8
> 
> Server URL : (give Your Sonar Server URL )
> 
> Add Sonar Server Token ( Token We Should add As Secrete Text )
> 
> Save it

**Configure SonarQube Server Scanner**

* Click on Manage Jenkins
    
* Click on Global Tools Configuration
    
* Click on SonarQube Scanner
    

> Name : Sonar -Scanner-4.7
> 
> Select Sonar Version (Sonar -Scanner-4.7)
> 
> save it

### Create Jenkins Pipeline

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721754659149/244b9a91-b57d-4a80-b73c-3523e72d7120.jpeg align="center")

```bash
pipeline {
    agent any
    
    environment {
        PATH = "$PATH:/opt/apache-maven-3.8.8/bin" // Corrected Maven path
    }
    
    stages {
        stage("GetCode") {
            steps {
                git "https://github.com/divyasatpute/java-maven-app.git"
            }
        }
        
        stage("Build") {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage("SonarQube Analysis") {
            steps {
                withSonarQubeEnv('sonarqube-8.4') {
                    sh "mvn sonar:sonar"
                }
            }
        }
    }
}
```

**<mark>Run Job</mark>**

* click on New Item
    
* Give Name----&gt;&gt; Select Pipeline ----&gt;Click on OK
    
* Paste Pipeline
    
* Apply and Save
    

### Here are my some test Results

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721754389043/2778c472-b3c3-4458-a2ef-9b0b48953cf3.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721754412528/223f1c0e-68b3-40c2-bda5-189f2e4508aa.jpeg align="center")

### **Hurray you completed this project**

**Hurray! Celebrating Successful Jenkins and SonarQube Integration! 🚀**

Congratulations on setting up Jenkins and SonarQube integration smoothly! 🎉 This achievement highlights your dedication to improving code quality and streamlining development processes. With Jenkins orchestrating builds and SonarQube providing insightful code analysis, your team is empowered to deliver high-quality software efficiently.

Keep up the fantastic work! 🌟 Here's to more milestones and continuous improvement in your software development journey. Cheers to innovation and excellence! 🥂

**NOTE: if you face some issue comment below and connect with me on Linkdin @**[**https://www.linkedin.com/in/divya-satpute-68666a300/**](https://www.linkedin.com/in/divya-satpute-68666a300/)