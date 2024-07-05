---
title: "Mastering Jenkins: A Full Guide"
seoTitle: "Jenkins Mastery: Complete Guide"
seoDescription: "Master Jenkins with this comprehensive guide on installation, configuration, creating jobs, and integrating with GitHub, Maven, and Tomcat server"
datePublished: Fri Jul 05 2024 15:23:41 GMT+0000 (Coordinated Universal Time)
cuid: cly8uiecw000e09l6870g7dma
slug: mastering-jenkins-a-full-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720192618038/9a38757f-3553-40b6-b95c-4a9e540f12ba.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720192980175/55c2c66e-29e1-4055-9b36-21c4ebd1293a.png
tags: aws, devops, jenkins, cicd, devops-articles, tws, diu

---

### Jenkins: An Overview 🌟

**What is Jenkins?**

Jenkins is an open-source automation server that enables developers to build, test, and deploy their software. It’s a cornerstone tool in the field of continuous integration (CI) and continuous delivery (CD).

**How Does Jenkins Work?**

1. **Source Code Management Integration:** Jenkins pulls the latest code from version control systems (e.g., GitHub, Bitbucket).
    
2. **Build Automation:** It compiles the code and packages it into an executable format.
    
3. **Testing:** Jenkins runs automated tests to ensure the code is stable and bug-free.
    
4. **Deployment:** It deploys the code to the production environment or a staging server.
    
5. **Monitoring and Notifications:** Jenkins provides real-time feedback and notifications to the development team about the build status.
    

**Benefits of Using Jenkins:**

1. **Improved Code Quality:** Automated testing helps catch bugs early in the development process.
    
2. **Faster Delivery:** Continuous integration and delivery speeds up the release cycle.
    
3. **Increased Productivity:** Automation frees up developers to focus on writing code rather than manual tasks.
    
4. **Collaboration:** Jenkins facilitates better collaboration between development and operations teams.
    

**Getting Started with Jenkins:**

1. **Installation:** Jenkins can be installed on various operating systems including Windows, macOS, and Linux.
    
2. **Configuration:** Set up your Jenkins server, configure the necessary plugins, and connect it to your version control system.
    
3. **Creating Pipelines:** Define your build, test, and deployment pipelines using Jenkins-file, a text file that contains the pipeline definition.
    

here is useful commands for install Jenkins

### **Prerequisites for Using Jenkins 🌟**

* A machine with at least 256 MB of RAM (recommended: 1 GB or.......
    
* Java installed on your machine
    

**commands for installation Jenkins on ubuntu Linux machine**

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

for start Jenkins use following commands

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

Open your EC2 instance public IP (https://&lt;public\_IP&gt;:8080/) along with port 8080 in your favorite browser. And provide the administration password obtained during the installation.

> Note: Make sure you enable 8080 port in Security Group Inbound Rules.
> 
> Get the initial administration password
> 
> ```bash
> $sudo cat /var/lib/jenkins/secrets/initialAdminPassword
> ```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720175911910/f3b5cf23-23f7-4bce-97e3-72e00373564b.jpeg align="center")

**Now your Jenkins started : <mark>Create Admin user</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720175954747/e82cbef6-f72e-455c-a03d-2d04b8ad3a36.jpeg align="center")

**🎉🎉Now , appreciate yourself you successfully deploy Jenkins on your machine 🎉🎉**

its is Look like this **: <mark>Jenkins up and Running</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720176148435/7053e99f-af62-4c7c-9daa-e59ebb0955d9.jpeg align="center")

---

Now moving towards advance concepts ----&gt;&gt;&gt;&gt;&gt;&gt;&gt;

Now we want to create <mark>job</mark> in Jenkins

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720176234044/d73ba11b-e95a-4c91-afda-9c1cb96d8808.jpeg align="right")

### Steps for create job in Jenkins

**Jenkins Job with <mark>GIT HUB</mark> Repo + <mark>Maven</mark> + <mark>Tomcat server </mark> Integration and Deployment**

### Pre-Requisites : Java , Git , and Maven

Git installation :

```bash
$sudo apt install git -y
```

**JDK Installation :**

In your Jenkins Dashboard -&gt; Manage Jenkins -&gt; Global tools configuration -&gt; Add JDK -&gt; Choose JDK 8 -&gt; Configuration Oracle Account Credentials

**Maven Installation :**

Jenkins Dashboard -&gt; Manage Jenkins -&gt; Global tools Configuration -&gt; Add Maven

**Plugin Installation :**

Jenkins Dashboard -&gt; Manage Jenkins -&gt; Manage Plugins -&gt; Goto Available -&gt; Search for "Deploy Container" Plugin -&gt; Install it .

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720187086433/16229882-1208-4ee0-a2e0-eed3cd2d2433.jpeg align="center")

> what we done so far ??? ----&gt;&gt; install git in our machine and <mark>in</mark> Jenkins we install maven , JDK , and plugins ....we all set for creating Jenkins Job

### Sample Git Repo URLS For Practice

<mark>Git Hub Repo URL</mark> : [https://github.com/divyasatpute/maven-jenkins-app-.git](https://github.com/divyasatpute/maven-jenkins-app-.git)

Now go to your tomcat server and configure below users in " tomcat-users .xml" file (it will be available in tomcat server conf folder )

```bash
<role rolename="manager-gui" />
<user username="tomcat" password="tomcat" roles="manager-gui" />
<role rolename="divya-gui" />
<role rolename="manager-script"/> 
<user username="divya" password="divya" roles="manager-gui,divya-gui, manager-script"/>
```

> Now create Jenkins job (step for create )

1. New **Item** :
    
2. Enter Item Name (**Job Name** )
    
3. Select **Free Style Project** & **Click OK**
    
4. Enter Some **Description**
    
5. Go to "**Source Code Management** " Tab and Select "**Git**"
    
6. Enter Project "**Git Repo URL** "
    
7. Add Your **Git-hub Account Credentials**
    
8. Go to "**Build Tab** "
    
9. Click On Add "**Build"** Step And Select " **Invoke Top Level Maven Targets** "
    
10. Select **Maven** and Enter Goals "**clean package**"
    
11. Click On "**Post Build Action** " and Select "**Deploy War /Ear to Container**" Option
    
12. Give **path** of war file (you can give like this also : **\*\*/\*. war** )
    
13. Enter Context Path (**Give your Project Name** )
    
14. Click On "**Add Container**" and Select **Tomcat Version 9.x**
    
15. Add Tomcat Server Credentials (**Give Username and password which is having manager-script role** )
    
16. Enter Tomcat Server URL (**http://EC2-VM-IP :Tomcat server Port)**
    
17. Click On **Apply** and **Save .**
    

> Heyyy buddyyy , look you able to all : Here’s a quote for you
> 
> "Congratulate yourself for the journey you’ve undertaken, for the progress you’ve made, and for the strength you’ve shown. Every step forward is a victory worth celebrating.🌟👏🎉"

## What are Jenkins jobs?

Jobs are the heart of *Jenkins's build* process. A job can be considered as a particular task to achieve a required objective in *Jenkins*. Moreover, we can create as well as build these jobs to test our application or project. *Jenkins* provides the following types of build jobs, that a user can create on a need basis. Consequently, the following image highlights a few of the *Jenkins build jobs*, which are used very frequently these days:

\*\*Let's understand the details of these various types of *Jenkins build jobs*:  
\*\*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720189790127/d120d299-15ce-4cd6-b0c6-d035ec133e7a.jpeg align="center")

### ***How to create a job in Jenkins?***

***Step 1***: Firstly, login into *Jenkins* account with valid credentials. After that, click on the "***New Item***"  option in *Jenkins dashboard*.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720190301195/a97c269d-bc9e-417e-be55-9fb67fe2fdaf.jpeg align="center")

As soon as, we will click, we will be redirected to a new page where we need to fill in the name of the job and select the type of job.

***Step 2***: Secondly, let's create a ***Freestyle project*** to build and run the project stored in the [***GitHub repository***](https://github.com/toolsqa17061989/DemoJava):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720190561736/976c2aa2-5ba4-4513-95c5-336030ca2df7.jpeg align="center")

* *First, enter the item name.*
    
* *Second, select the project type ( I selected the Freestyle project).*
    
* *Third, click on the Ok button.*
    

As soon as we click on the OK button, the *Jenkins Job* will be created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720190751768/2bcbe278-2238-4275-8d07-4f82a21e3c8e.jpeg align="center")

So, in this way Job can be created in Jenkins. in the next section, we will see how to configure this newly created job.

### ***How to configure a job in Jenkins?***

In the previous section, we created a FreeStyle job in Jenkins. Let's see in this section that how to configure the above created Jenkins build job? Kindly follow the below steps:

***Step 1***: First, select the "***Configure***"  option that is shown in the dropdown in the below image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720190863078/0afcc817-532a-40f4-a167-bb94261316c2.jpeg align="center")

Moreover, as soon as we will click on the configure option then we will redirect towards the ***Configuration*** page.

***Step 2***: Secondly, set the purpose of the job in the "***Description***"  section.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720191104374/4820a163-89ca-4dcb-9a7b-1f4ee1abc66b.jpeg align="center")

Apart from the description, there will be some options in the *General section*. Let's shortly see those options:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720191196174/7d6212cb-b747-48ca-94ed-9bb4e00eb9c7.jpeg align="center")

***Step 3***: Thirdly, in the ***Source Code Management*** section, we need to select the repository where we pushed our code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720191268657/ac2f9c3f-cdbc-4368-aa93-474eae0d49a6.jpeg align="center")

As I pushed our code in the [***GitHub repository*** so I selected the](https://github.com/toolsqa17061989/DemoJava) Git option in the above image.

***Step 4***: Fourthly, go to the "***Build triggers***"  [section and selec](https://github.com/toolsqa17061989/DemoJava)t the appropriate option as per requirements. There are different options available here under the build triggers section.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720191362582/8f763c88-68b9-4cfe-bc3a-492f94fab42e.jpeg align="center")

Let's understand the details of all these options:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720191431756/0c02a750-e43f-4778-b320-0bdeebad95dc.jpeg align="center")

***Step 5***: Fifthly, go to the "***Build***"  section. In this section, there are ***some most popular options***  available that are listed in the below table:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720191532034/144599a0-4461-4de4-94c6-59ea8e6bc488.jpeg align="center")

<mark>Now click save and apply</mark>