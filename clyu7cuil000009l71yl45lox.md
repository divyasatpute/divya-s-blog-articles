---
title: "🚀 SonarQube Tutorial: Improve Your Code Quality🐞"
seoTitle: "SonarQube Guide: Enhance Code Quality"
seoDescription: "Learn how to enhance your code quality with SonarQube, a comprehensive guide from setup to integration"
datePublished: Sat Jul 20 2024 14:06:27 GMT+0000 (Coordinated Universal Time)
cuid: clyu7cuil000009l71yl45lox
slug: sonarqube-tutorial-improve-your-code-quality
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721476616776/d47c2bd0-3e5c-4daf-a3a8-161fcf2ab619.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721484356550/419620dd-28ec-4593-be4f-8c6554b09e4b.png
tags: sonarqube, devops, distributed-system, devops-articles, tws, diu

---

### Table of Contents🔄🧐

* What is SonarQube ??
    
* what is Code Review ??
    
* How To Setup Sonar Server ??
    
* Sonar Admin logins??
    
* Sonar Rules ??
    
* Sonar Quality Profile and Making Custom Quality Profile as default ??
    
* Using Sonar Quality Profile and Custom Quality Profile as a particular Project ??
    
* Sonar Quality Gate ??
    
* Integrated Sonar Server With Java Maven app ??
    
* Sonar Token Generation
    
* Conclusion 🌊
    

### 🦸‍♂️ What is SonarQube? 🚀

* SonarQube is an open-source platform that helps developers manage code quality and security. It provides insightful metrics and continuous inspection for your codebase. Here’s a quick overview:
    
* SonarQube is Continuous Code Quality Checking Tool
    
* We can do code Review using SonarQube Tool
    
* SonarQube is an open source Software Quality Management Tool
    
* It will continuously analyze and measures quality of the source code
    
* It will be generate code review report in html format /pdf format
    
* It is web based tool and it support 29 programming languages
    
* It will be support multi OS platform
    
* It will be support multiple databases (MySQL, Oracle , SQL server .......)
    
* It supports multiple Browsers
    
* Initially SonarQube was developed only for java projects
    
* Today SonarQube is supports 29 programming languages
    

*SonarQube will identify <mark>below category of issue i</mark>n project source code*

1. Duplicate code
    
2. Coding Standards
    
3. Unit Tests
    
4. Code Coverage
    
5. Complex Code
    
6. Commented Code
    
7. Potential Bugs
    

### What is Code Coverage & Code Review📜

* **<mark>Code Coverage </mark>** : How many lines of source code is tested by Unit test Cases
    

> NOTE : Industry standard code coverage is 80 %

* **<mark>Code Review</mark>** : Checking Coding Conventions
    
    ### 🌟 Key Features:
    
    * **Code Quality** 📝: Automatically checks your code for bugs, vulnerabilities, and code smells.
        
    * **Continuous Integration** 🔄: Integrates seamlessly with CI/CD pipelines, ensuring quality checks with every commit.
        
    * **Multi-Language Support** 🌐: Supports over 25 programming languages, making it versatile for any project.
        
    * **Real-time Feedback** ⚡: Developers receive immediate feedback on code quality to encourage best practices.
        

### Environment Setup🖥️

**<mark>Pre-requites:</mark>**

Java is installed on your Machine

if SonarQube 7.6 ----&gt; Java 1.8 version is installed

if SonarQube 7.6 -----&gt; java 11 version is Installed

> Note : We can Check this Compatability in official SonarQube Website

**Hardware Requirements**

Minimum RAM : 2 GB

### 🌐 SonarQube Architecture Diagram

```plaintext
         +------------------+
         |   🌍 SonarQube    |
         |   Web Interface   |
         +------------------+
                 |
                 ▼
         +------------------+
         |   🏢 SonarQube    |
         |     Server       |
         +------------------+
                 |
                 ▼
         +------------------+
         |   🗄️ Database     |
         | (PostgreSQL,    |
         |  MySQL, etc.)   |
         +------------------+
                 |
                 ▼
         +------------------+
         |   ⚙️ Compute      |
         |     Engine       |
         +------------------+
                 |
                 ▼
         +------------------+
         |   📦 SonarQube    |
         |     Scanner      |
         +------------------+
                 |
                 ▼
         +------------------+
         |  🔌 Plugins       |
         |   (Extensions)   |
         +------------------+
```

### ⚙️Step for deploy SonarQube

Create EC2 Instance with 4 GB Ram (t2.medium )

Connect with EC2 instance using Git-Bash

Switch to Root User

```bash
sudo -i
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

"Congratulations to yourself! Celebrate your achievements and continue to shine."

<mark>you did it </mark> !!!! Now your SonarQube started it look like this :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721322863939/36d66f8d-109e-4dcd-b187-157be1059866.jpeg align="center")

**Access your SonarQube :**

URL : http : // EC2-VM-Public-IP :9000/

> Note : SonarQube runs on 9000 port by Default . Enable this port in security group as custom TCP

SonarQube Dashboard look like this :

> Note : Default login id and password is **<mark>admin</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721397120528/48b15089-336f-46b2-ab51-252a24674b32.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721394003328/17d97eb6-8557-4821-b103-98a6687b2589.jpeg align="center")

---

### 🖥️Integrated Sonar Server With Java Maven app

Configure Sonar Properties Under &lt;Properties/&gt; tag in pom.xml

```bash
#<sonar.host.url>sonar-server-url</sonar.host.url>
#<sonar.login>username</sonar.login>
#<sonar.password>pwd</sonar.password>

#paste your value here:
<properties> 
<sonar.host.url>http://23.23.2.151:9000</sonar.host.url>
<sonar.login>admin</sonar.login>
<sonar.password>admin</sonar.password>
</properties>
```

Go to Project pom.xml file location and execute below goal in command Promt

```bash
mvn sonar:sonar
```

After Build Success go to Sonar Dashboard and verify that

> Note : **<mark>Instead of Username And Password We can Configure Token Also</mark>**
> 
> **<mark>Because it is not Recommended way to configure login id and password</mark>**
> 
> **<mark>for Security Purpose you can use token instead of password</mark>**

**Steps configure Token**

Go to Sonar ---&gt;Login ---&gt; Click On profile ----&gt; My Account ---&gt; Security ---------------&gt;Generate Token

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721405799926/3f97af35-cad4-43a5-98ac-8efd43c86f57.jpeg align="center")

Copy the Token And Configure that in pom.xml like below

```bash
#<sonar.host.url>sonar-server-url</sonar.host.url>
#<sonar.login>token</sonar.login>
#paste your value here :
<properties> 
<sonar.host.url>http://23.23.2.151:9000</sonar.host.url>
<sonar.login>fcc13f88143e48d81ee1328cc855b89132ea8817</sonar.login>
</properties>
```

Then build the Project using "**<mark>mvn sonar:sonar</mark>**" goal

you got result like this :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721403549131/49aec597-20b3-4a63-882d-4a1ef29d9cd3.jpeg align="center")

**And you can see your Dashboard and report will be generated**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721403636279/a5ded061-57ed-49fc-95ff-ceed1e721957.jpeg align="center")

---

### 📚Quality Profile in SonarQube

Quality profile means set of rules to perform code review

For each language SonarQube provided one Quality Profile

We can create our own quality profile based on Requirement

create one own Quality profile

$ Name : SBI project

$ language :java

$ parent : none

![A screenshot of the SonarQube web interface. The "Quality Profiles" section is highlighted in red. In the center, a "New Profile" popup is open, with fields for "Name" (filled with 'H2 project'), "Language" (selected as Java), and "Parent" (set to None). Two buttons labeled "Create" and "Cancel" are at the bottom of the popup. The "Create" option in the upper right corner is also highlighted. Note: The user's Windows taskbar is visible with various application icons.](https://cdn.hashnode.com/res/hashnode/image/upload/v1721404647506/dca93094-aeab-4dbd-853e-c33bbaca8a8e.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721405197267/baea9a6b-6fbd-403a-8115-99168d4f7c78.jpeg align="center")

> by clicking <mark>Activate more</mark> , you can add costem rules according your requirement
> 
> Note : If we have any common ruleset for all projects then we can create one own quality profile and we can use that as parent quality profile for other profiles

we can also configure quality profile to specific project only

* click on project name
    
* go to administration
    
* click on quality profile
    
* select profile required
    
* ![A screenshot of a terminal window shows output logs from a Maven web application build process. The logs include time-stamped [INFO] messages indicating steps such as executing project builders, loading quality profiles, indexing files, configuring the project, and loading metrics repositories. quality profile they took default .](https://cdn.hashnode.com/res/hashnode/image/upload/v1721405357457/148130ed-1b02-437d-abfc-6fbd89e3ddeb.jpeg align="center")
    
    above image they took <mark>default</mark> Quality profile
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721406116878/da0be44c-645c-423a-b7e0-38cc9a35c954.jpeg align="center")

> Note : you can see above image our custom quality profile created go to settings and set it default

when we create custom quality profile name called "H2 project " then we took our quality profile like this we can create custom quality profile according to requirement

> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721411046753/88e171c0-db06-4c29-bc64-30d4524fac65.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721411372318/fbd5f969-6af8-404f-a5fa-89460c82380f.jpeg align="center")

> Note : The [**38\_SB\_REST\_H2\_DB\_APP** project cr](http://23.23.2.151:9000/dashboard?id=in.ashokit%3A38_SB_REST_H2_DB_APP)ea[te code review using](http://23.23.2.151:9000/dashboard?id=in.ashokit%3A38_SB_REST_H2_DB_APP) **<mark> Token </mark>** and custom **<mark>Quality Profile</mark>**
> 
> The [**my-webapp Maven Webapp**project create code r](http://23.23.2.151:9000/dashboard?id=com.example%3Amy-webapp)eview using **<mark>login id</mark>** and **<mark>password</mark>** and **<mark>default Quality profile</mark>**

---

### Quality Gate🔒

Quality Gate represent set of metric to identify project quality is passed or failed

Every Project Quality Gate Should be Passed

In Sonar we have default Quality Gate

If required , we can create our own Quality Gate also

> Note : <mark>If the project Quality Gate is </mark> **<mark>failed </mark>** <mark>then we should not Accept that code for deployment</mark>

### Conclusion 🌊

SonarQube isn't just about analyzing code—it's about elevating your development process and delivering exceptional software. Embrace SonarQube to unlock the true potential of your projects and sail towards a future where quality meets innovation.

### Ready to Set Sail? ⛵

Start your journey with SonarQube today and discover the joy of coding with confidence. Let SonarQube be your guiding star 🌟 towards cleaner, safer, and more efficient code.

### Thanks a lot! 🎉 Celebrating achievements, big or small, is important.