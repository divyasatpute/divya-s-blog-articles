---
title: "Introduction to Jenkins: What You Need to Know"
seoTitle: "Jenkins Basics: Essential Guide"
seoDescription: "Dive into Jenkins and learn the essentials of CI/CD, build and deployment processes, and best practices. Start automating with Jenkins today! 🚀"
datePublished: Sun Jun 30 2024 14:00:25 GMT+0000 (Coordinated Universal Time)
cuid: cly1mc20700000ak1e9mkbuxi
slug: introduction-to-jenkins-what-you-need-to-know
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719742584369/d78e302b-fea6-44de-8635-c83ccbfd252f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1719755987336/ae9f2603-7959-49ef-befb-c41a28f67f13.png
tags: devops, jenkins, trainwithshubham, tws, diu

---

Hey there! 🎉 Ready to dive into Jenkins? Whether you're new to CI/CD or just need a refresher, this guide will help you get started with Jenkins. Let's go! 🚀

### Introduction to Jenkins 🚀

* **What is Jenkins?** 🤔
    
    * Jenkins is an open-source automation server.
        
    * It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery (CI/CD).
        
    * Jenkins is an open-source automation for CI-CD
        
    * Jenkins tools developed using java
        
    * Jenkins is part of Hudson Project
        

**Initially it is called as <mark>Hudson</mark> then later it renamed to <mark>Jenkins</mark>**

🎬**About CI CD**

* CI and CD are two most frequently used terms in modern development practices and DevOps practices
    
* CI stands for continuous Integration. It is fundamental DevOps best practices where developers frequently merge code changes to central repository where automated builds and tests runs.
    
* CD means Continuous Delivery or Continuous Deployment.
    

Jenkins is a self-contained, open-source automation server which can be used to automate all sorts of tasks related to building, testing, and deploying software.

### 🌐🔍Build and deployment Process

1. Take latest source code from Repository
    
2. Compile source code
    
3. Execute Unit tests (Junit)
    
4. Perform code Review
    
5. Package code as a war file
    
6. Deploy the war file into server
    

> Note : All the above builds and deployment tasks can be automated using Jenkins tool.

**<mark>Key Features of Jenkins</mark>** <mark> 🔑</mark>

* **<mark>Extensible:</mark>** Supports a wide range of plugins for integration with various tools and services.
    
* **<mark>Distributed Builds</mark>:** Can distribute builds and tests across multiple machines for faster execution.
    
* **<mark>User-Friendly</mark>:** Provides a simple and intuitive web-based interface.
    
* **<mark>Scalable:</mark>** Easily scales up for large projects and teams.
    

**<mark>Community Support</mark>:** Boasts a large and active community, providing a wealth of plugins, tutorials, and help.

**Why Use Jenkins? 🛠️**

* **Automation:** Reduces manual efforts by automating repetitive tasks.
    
* **Consistency:** Ensures consistent build and deployment processes.
    
* **Speed:** Accelerates development and deployment cycles.
    
* **Quality:** Enhances code quality by running automated tests.
    
* **Integration:** Seamlessly integrates with other tools and services.
    

### Prerequisite (Step 1 )

* Jenkins installation on AWS EC2
    
* Create an EC2 instance with ubuntu Linux AMI
    
* Connect to your EC2 instance
    
* Update all packages by following command :
    

```bash
$sudo apt update -y
```

* Install java by following command :
    

```bash
sudo apt install openjdk-11-jdk -y
```

### Step 2

Jenkins installation on AWS EC2 Using apt

Add Jenkins to your apt Repository using following command

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

Import a key file from Jenkins -CI to enable installation from the package

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
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

### 🛤️ Creating Your First Job

1. **New Item**:
    
    * Click on `New Item` in the Jenkins dashboard.
        
2. **Name Your Job**:
    
    * Enter a name for your job and select `Freestyle project`.
        
3. **Configure Your Job**:
    
    * **Source Code Management**: Link your job to a version control system like Git.
        
    * **Build Triggers**: Set when the job should run (e.g., after a commit).Give Build Tigger Periodically
        
        \* \* \* \* \*
        
    * **Build**: Define the build steps, such as compiling code or running tests.
        
4. **Save and Build**:
    
    * Save your job and click `Build Now` to run it.
        

> Note: 5 \* stars represents every minute Jenkins Job Should Execute

Configure Below Script as a Build Script

```bash
echo "Hello Guys, Divya Here" 
touch divya.txt
echo "Hello Guys, Welcome to learnwithdivya.online" >> divya.txt
echo "Done ..!!"
```

### 🚀 Tips and Best Practices

* **Backup Regularly**: Ensure you have backups of your Jenkins configuration and jobs.
    
* **Use Pipelines**: Pipelines provide a powerful way to define your build process as code.
    
* **Keep Jenkins Updated**: Regular updates bring new features and security improvements.
    

### 🎉 Conclusion

Jenkins is a powerful tool that can supercharge your development workflow. By automating builds, tests, and deployments, it frees up your time and helps you focus on what really matters – writing awesome code! 🧑‍💻💪

Happy building with Jenkins! 🚀✨

Here my POC Results for you :

<mark>CLI output Jenkins Started</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719509828953/e51f4de0-03df-4d62-9d4b-e0f22eb468c0.jpeg align="center")

<mark>Creation 1st job</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719509847630/63f5192a-37fb-4fc2-9412-8229520ccb71.jpeg align="center")

<mark>Console Output</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719509868680/2e68a7ee-fdc5-4850-bee4-fd75e1eadb75.jpeg align="center")

<mark>Build got succuss</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719509882209/3992d8df-5664-407a-b4b9-d1be96a62c3e.jpeg align="center")