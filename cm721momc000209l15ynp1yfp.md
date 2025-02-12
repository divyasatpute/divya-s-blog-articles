---
title: "Lift And Shift Application Workload ( AWS Project )"
seoTitle: "AWS Project: Lift & Shift Workload"
seoDescription: "Use Lift and Shift to move apps to AWS for better scalability, security, and cost-efficiency. Set up EC2, DNS, and load balancing"
datePublished: Wed Feb 12 2025 15:05:56 GMT+0000 (Coordinated Universal Time)
cuid: cm721momc000209l15ynp1yfp
slug: lift-and-shift-application-workload-aws-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739372449582/f12f5f1c-f68d-4d26-9ffd-c86511fba4bc.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1739372738453/ba7881d5-6a6d-4259-a27a-856373ca969a.jpeg
tags: webapps, aws, projects, devops, tws, diu, teacode

---

## About this project

1. Multi Tier Web Application Stack \[VProfile \]
    
2. Host And Run on AWS cloud for production
    
3. Lift and shift strategy
    
    > ***Before getting started, let’s understand what is Refactoring strategy.***
    
    Refactoring is one of the strategies for migrating applications to AWS. It involves re-architecting workloads to support AWS cloud-native capabilities from the ground up. This strategy requires a significant investment in effort and resources but is considered the most future-proof migration approach. The outcome of refactoring is a cloud-native application that fully exploits cloud innovation.
    
    > ***Benefits of the migrating application using Refactoring strategy.***
    
    Some benefits of refactoring include long-term cost reduction by matching resource consumption demand and eliminating waste. This can result in a better return on investment compared to less cloud-native applications. Refactoring can also increase resilience by decoupling application components and using highly-available AWS-managed services. Additionally, refactored applications can be more responsive to business events and can exploit AWS innovation.
    

## **Introduction**

* Briefly introduce the concept of a **Multi-Tier Web Application**.
    
* Explain the **Lift and Shift Strategy** and why it’s useful for migrating applications to AWS.
    
* Introduce **VProfile** as the application you are migrating.
    

#### **📌 Scenario Overview**

You have an application stack running in your **on-premises data center**, utilizing a mix of **physical and virtual machines**. The stack includes:

🔹 **Windows Server** – Hosting various enterprise applications  
🔹 **DNS** – Providing name resolution services  
🔹 **Oracle Database** – Managing structured data  
🔹 **LAMP Stack** – Running PHP-based applications  
🔹 **Java & Tomcat** – Backend microservices  
🔹 **NGINX+** – Load balancing and reverse proxy  
🔹 **PHP** – Web-based applications

To modernize and improve **scalability, security, and cost-efficiency**, we will migrate this workload to **AWS using the Lift and Shift approach**.

## **☁️ Migration Strategy: Lift and Shift to AWS**

The **Lift and Shift Strategy** moves applications **without refactoring**, ensuring a fast and smooth migration to AWS.

# Problem And Challenges

#### **⚠️ Challenges of On-Premises Infrastructure**

Organizations running applications on **on-premises physical/virtual machines** often face several operational bottlenecks. Let’s explore the key challenges:

### **🚧 Problems with On-Premises Infrastructure**

🔴 **Complex Management**

* Managing multiple servers, databases, and networking components is **time-consuming** and requires **manual intervention**.
    
* Dependency tracking and troubleshooting are **difficult** in a distributed environment.
    

🔴 **Scalability Limitations**

* Scaling infrastructure up or down based on demand is **complex and expensive**.
    
* Requires **manual hardware provisioning** and **capacity planning** to avoid under/overutilization.
    

🔴 **High Upfront & Operational Costs**

* **Capital Expenditure (CapEx)**: Heavy initial investment in hardware, networking, and storage.
    
* **Operational Expenditure (OpEx)**: Recurring costs for maintenance, electricity, cooling, and IT personnel.
    

🔴 **Manual & Time-Consuming Processes**

* Setting up new servers, deploying applications, and maintaining infrastructure is **manual and error-prone**.
    
* **Lack of automation** leads to slower deployment cycles and **inconsistent configurations**.
    

🔴 **Difficult to Automate & Maintain**

* Legacy applications often require **custom scripts** for deployment.
    

**Monitoring, patching, and backup** processes require manual effort.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739173989353/7b902c9c-78f4-40a9-9536-d6961bfaf9ec.png align="center")

# Solution

## **✅ Solution: Lift and Shift to AWS**

### **<mark>GitHUB REPO</mark>** : [https://github.com/divyasatpute/vprofile-awsliftshift-project](https://github.com/divyasatpute/vprofile-awsliftshift-project)

Migrating to **AWS using a Lift and Shift approach** resolves these challenges while ensuring **scalability, security, and cost optimization**.

### **AWS Cloud Setup (After Migration)**

🔹 **Compute Layer (EC2 & Scaling)**  
✅ Amazon EC2 for running Tomcat, RabbitMQ, MySQL, Memcached  
✅ Auto Scaling Groups for dynamic VM scaling  
✅ Elastic Load Balancer (ELB) for distributing traffic

🔹 **Storage & Data Layer**  
✅ Amazon EFS (Elastic File System) for **shared storage** across VMs  
✅ Amazon S3 for storing logs, backups, and assets  
✅ Amazon RDS (MySQL) for relational database migration

🔹 **Networking & Security**  
✅ **Amazon Route 53** for **Private DNS Service** and domain resolution  
✅ **NGINX Replacement** with AWS ELB for traffic balancing  
✅ Security Groups & IAM Roles for controlled access

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739174059543/17fd8c16-a3c6-4f16-b846-94c202b396e4.png align="center")

# FLOW OF EXECUTION

1. Login to AWS Account
    
2. Create Key Pairs
    
3. Create Security groups
    
4. Launch Instances with user data \[BASH SCRIPTS\]
    
5. Update IP to name mapping in route 53
    
6. Build Application from source code
    
7. Upload to S3 bucket
    
8. Download artifact to Tomcat Ec2 Instance
    
9. Setup ELB with HTTPS \[Cert from Amazon Certificate Manager\]
    
10. Map ELB Endpoint to website name in Hostinger DNS
    
11. Verify
    
12. Build Autoscaling Group for Tomcat Instances.
    

# <mark>Step by Step Guidance</mark>

Create security group for load-balancer

Click on EC2

Go to Security Group

Give Name and description

Allow HTTP:80 IPv4, IPv6

Allow HTTPS:443 IPv4 , IPv6

Click On Create Security Group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739175295317/d04289f9-91bb-4d6e-bd55-6c6a74cf0db4.png align="center")

**2nd Security Group For App**

Click on EC2

Go to Security Group

Give Name and description

Allow custom TCP : 8080 and select loadbalancer group which we created before

Allow Custom TCP :22 and select My IP

Click On Create Security Group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739175913579/21489485-a2fb-4d9e-8f80-19b747b791e0.png align="center")

**3nd Security Group For App**

Click on EC2

Go to Security Group

Give Name and description

Allow MySQL/Aurora , make sure to select source section app security group which we created before

Allow Custom TCP :11211 , make sure to select source section app security group which we created before

Allow Custom TCP :5672 , make sure to select source section app security group which we created before

Allow Custom TCP :22 source : My IP

Click On Create Security Group

After adding security Group edit inbound rule

Allow All Traffic and source code select backend itself

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739176552658/b9c93e4b-4b0a-457c-992f-33ee6b9a3d85.png align="center")

> Note : If You Don’t know where this port are coming from check out GitHub- repo
> 
> \[ Vprofile-Project / src/Main/Resource/Application Properties \] in this location you will got all ports

### <mark>Now Create KEY-PAIR</mark>

Go To key-pair

Give name , and .pem format if you use gitbash

Create key pair

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739180830230/5221f0b5-29f7-4121-94d8-518955134d36.png align="center")

## <mark>Setting-up EC2 instances</mark>

Now we are going to set -up 4 EC2 instances one for MYSQL , 2nd for Memcache and 3rd for RabbitMQ and 4 Th for Tomcat server

We are going to provision this instance and set up all the services by using the userdata script.

And while we launch these instances, we have to make sure we put them in the right security group.

These three instances goes into back end security group. Tomcat instance goes into the app security group.

First thing we'll do is we will clone our source code.

```bash
git clone https://github.com/hkhcoder/vprofile-project.git
```

## <mark>Launch Instance for MYSQL</mark>

Go to AWS account

Click On Launch Instance

Give Name and Provide Tag also , so you can follow correct standards

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182342969/3b8b42cc-ce95-4fb1-aa67-7824ca349b87.png align="center")

Select AMI Linux 2023

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182402998/e4bcd3b0-b715-4f70-8fe8-52aa4c4c264b.png align="center")

**<mark>Instance Type T2 micro</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182451401/bca5549b-ca73-48ef-b6b6-c12348ac152f.png align="center")

select Key pair which we created at 1st

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182500858/7d183766-b363-40c2-b02a-aaf3eb10f0c9.png align="center")

on network setting select for MYSQL backed security group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182576754/8fab866a-1230-4bd9-9116-c75d1df55ac6.png align="center")

in Advanced setting go to user data section and paste script which is available in github userdata mysql.sh

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182750412/4316e0df-8f20-4348-95bc-b444ec0af609.png align="center")

This is MYSQL.sh also available on userdata mysql.sh

```bash
#!/bin/bash
DATABASE_PASS='admin123'
sudo dnf update -y
sudo dnf install git zip unzip -y
sudo dnf install mariadb105-server -y
# starting & enabling mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
cd /tmp/
git clone -b main https://github.com/hkhcoder/vprofile-project.git
#restore the dump file for the application
sudo mysqladmin -u root password "$DATABASE_PASS"
sudo mysql -u root -p"$DATABASE_PASS" -e "ALTER USER 'root'@'localhost' IDENTIFIED BY '$DATABASE_PASS'"
sudo mysql -u root -p"$DATABASE_PASS" -e "DELETE FROM mysql.user WHERE User='root' AND Host NOT IN ('localhost', '127.0.0.1', '::1')"
sudo mysql -u root -p"$DATABASE_PASS" -e "DELETE FROM mysql.user WHERE User=''"
sudo mysql -u root -p"$DATABASE_PASS" -e "DELETE FROM mysql.db WHERE Db='test' OR Db='test\_%'"
sudo mysql -u root -p"$DATABASE_PASS" -e "FLUSH PRIVILEGES"
sudo mysql -u root -p"$DATABASE_PASS" -e "create database accounts"
sudo mysql -u root -p"$DATABASE_PASS" -e "grant all privileges on accounts.* TO 'admin'@'localhost' identified by 'admin123'"
sudo mysql -u root -p"$DATABASE_PASS" -e "grant all privileges on accounts.* TO 'admin'@'%' identified by 'admin123'"
sudo mysql -u root -p"$DATABASE_PASS" accounts < /tmp/vprofile-project/src/main/resources/db_backup.sql
sudo mysql -u root -p"$DATABASE_PASS" -e "FLUSH PRIVILEGES"
```

<mark>Launch instance</mark>

## <mark>Launch Instance for Memcache</mark>

Go to AWS account

Click On Launch Instance

Give Name and Provide Tag also , so you can follow correct standards

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739183167224/190c5544-7a9a-42be-8a29-2dc4eee68380.png align="center")

Select AMI Linux 2023

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182402998/e4bcd3b0-b715-4f70-8fe8-52aa4c4c264b.png align="center")

Instance Type T2 micro

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182451401/bca5549b-ca73-48ef-b6b6-c12348ac152f.png align="center")

select Key pair which we created at 1st

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182500858/7d183766-b363-40c2-b02a-aaf3eb10f0c9.png align="center")

on network setting select for MYSQL backed security group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182576754/8fab866a-1230-4bd9-9116-c75d1df55ac6.png align="center")

in Advanced setting go to user data section and paste script which is available in github userdata memcache.sh

```bash
#!/bin/bash
sudo dnf install memcached -y
sudo systemctl start memcached
sudo systemctl enable memcached
sudo systemctl status memcached
sed -i 's/127.0.0.1/0.0.0.0/g' /etc/sysconfig/memcached
sudo systemctl restart memcached
sudo memcached -p 11211 -U 11111 -u memcached -d
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739183366765/251480fa-035c-47a5-9924-6916e1dd4491.png align="center")

<mark>Launch instance</mark>

## <mark>Launch Instance for RabbitMQ</mark>

Go to AWS account

Click On Launch Instance

Give Name and Provide Tag also , so you can follow correct standards

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739183639589/b023b152-7f58-4b6f-900b-0dd3d028bc87.png align="center")

Select AMI Linux 2023

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182402998/e4bcd3b0-b715-4f70-8fe8-52aa4c4c264b.png align="center")

Instance Type T2 micro

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182451401/bca5549b-ca73-48ef-b6b6-c12348ac152f.png align="center")

select Key pair which we created at 1st

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182500858/7d183766-b363-40c2-b02a-aaf3eb10f0c9.png align="center")

on network setting select for MYSQL backed security group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182576754/8fab866a-1230-4bd9-9116-c75d1df55ac6.png align="center")

in Advanced setting go to user data section and paste script which is available in github userdata RarbbitMq.sh

```bash
#!/bin/bash
## primary RabbitMQ signing key
rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc'
## modern Erlang repository
rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key'
## RabbitMQ server repository
rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key'
curl -o /etc/yum.repos.d/rabbitmq.repo https://raw.githubusercontent.com/hkhcoder/vprofile-project/refs/heads/awsliftandshift/al2023rmq.repo
dnf update -y
## install these dependencies from standard OS repositories
dnf install socat logrotate -y
## install RabbitMQ and zero dependency Erlang
dnf install -y erlang rabbitmq-server
systemctl enable rabbitmq-server
systemctl start rabbitmq-server
sudo sh -c 'echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config'
sudo rabbitmqctl add_user test test
sudo rabbitmqctl set_user_tags test administrator
rabbitmqctl set_permissions -p / test ".*" ".*" ".*"

sudo systemctl restart rabbitmq-server
```

<mark>Launch instance</mark>

## <mark>Launch Instance for Tomcat Server</mark>

Go to AWS account

Click On Launch Instance

Give Name and Provide Tag also , so you can follow correct standards

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739184006219/5c1dd414-ab25-41a3-b0cf-feafa85ba717.png align="center")

Select AMI ubuntu 2024

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739184068851/aac9dec3-d4cd-403e-a3f3-093140a2cf3d.png align="center")

Instance Type T2 micro

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182451401/bca5549b-ca73-48ef-b6b6-c12348ac152f.png align="center")

select Key pair which we created at 1st

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739182500858/7d183766-b363-40c2-b02a-aaf3eb10f0c9.png align="center")

on network setting select for tomcat server select app security group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739184226483/1f66a0f5-507e-4b43-97da-f172c9756e0c.png align="center")

in advanced setting

```bash
#!/bin/bash
sudo apt update
sudo apt upgrade -y
sudo apt install openjdk-17-jdk -y
sudo apt install tomcat10 tomcat10-admin tomcat10-docs tomcat10-common git -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739184288500/255b177d-b910-4296-b59a-e84261efb4a5.png align="center")

<mark>Launch instance</mark>

# Step 2

## <mark>DNS Route 53</mark>

create Hosted zone

click on Route 53 service go to hosted zone section

make sure Same name give if you changing name configure same as in application properties file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739195283703/f91bc913-e31c-401d-81ba-0ca82fa715c0.png align="center")

Create Record for db01 server

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739195682403/73a54683-7094-42a4-a61f-c8f757f0c020.png align="center")

Create Record for mc01 server

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739195808161/f7d8b6db-f7e8-4c61-9f61-845504df7838.png align="center")

Create Record for rmq01 server

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739195899523/a3f571e6-7b0c-4cb1-80a5-77365504d180.png align="center")

Create Record for app01 server

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739196353987/4f29da27-0a5c-4141-a833-06319f10804a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739196794271/cf56bca5-067e-43b8-8715-c0a74d08294d.png align="center")

After Connect your app01 machine on terminal and verify where your configuration is correct or not by following command

```bash
 ping -c 4 db01.vprofile.in
```

same verify all records which you created

# Step 3

## <mark>Build And Deploy Artifact</mark>

## <mark>Create Bucket</mark>

Go to AWS s3 bucket

click on create bucket

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739196990392/e46ac9c6-6dae-43d0-9dbe-1224053fa067.png align="center")

Go To IAM service

## <mark>Create user</mark>

Give Name and Give s3 full access and create User

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739197204002/86772ec3-d353-480d-8983-1098c71dc82a.png align="center")

## <mark>Create Access Key</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739197369180/b5e2b4d4-dda1-45fc-b953-736d1a2296ce.png align="center")

## <mark>Create Role</mark>

Go To IAM service

click on create Role

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739279207757/b0d53484-4897-4840-80e7-fe80fb1a07c3.png align="center")

Attach s3FullAccess Policy

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739279276034/dd8a87a5-8d85-4d2c-8f70-aa3b0aedfab8.png align="center")

And Enter Create

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739279339177/acfa3487-b551-4449-bdc3-2f0f832f519e.png align="center")

Now Attach This Role To App01 EC2 instance

Go To EC2 Instance select vprofile-app01

Click on Action

Click On Security

Click On IAM role

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739279525811/40ead715-316a-4c98-ba20-e42e32e8a903.png align="center")

Update IAM role

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739279587820/ae7159c9-7d38-4592-bc4f-61d3f892bae3.png align="center")

On Your application Properties File Edit Same Changes

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739279994113/7b3b3322-d287-461c-bb4a-e0f4a1e82bca.png align="center")

<mark>And save File</mark>

* Install Maven 3.9.9 version On your System
    
* Install Java 17 version On your system (according to compability change version )
    
* And Install AWS CLI
    

Package application

```bash
mvn clean package
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739283901088/95732a42-5c1b-430a-aac7-2aaa7fefeda4.png align="center")

```bash
cp /home/ubuntu/vprofile-project/target/vprofile-v2.war /var/lib/tomcat10/webapps/ROOT.war
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289057781/9f89d835-9046-4dfb-a284-f60c603ebf1a.png align="center")

## <mark>Create a Target Group</mark>

Go to EC2 instance click on target group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289358001/6a957a51-7f7b-4d4a-bcfd-bae259f8e783.png align="center")

Give name and port no 8080

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289400937/98b341e3-dcdb-4580-8bb4-bc241814760f.png align="center")

go to advanced health checking setting override 8080

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289513743/4a43c084-ce51-4ad0-a38f-33fc84f1b5cf.png align="center")

click on next

Check mark app01 instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289625667/acf41ba8-66e5-4a40-bdc6-bd5eee4aa579.png align="center")

click on include pending below

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289671522/37a75a34-91a2-4dac-b155-5bca9be12889.png align="center")

verify 8080 and hit create target group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289721642/2838a4e0-665d-4d4e-bd89-9c3ad63bb223.png align="center")

## <mark>Create Loadbalancer</mark>

Click on Create Loadbalancer

Click on Application Loadbalancer

Give Name

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739289992366/efc49100-cdf4-4920-972d-448a903cb8a2.png align="center")

Check mark all availability zones

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739290046358/0afb1907-2767-4853-9497-51e35d95aa7f.png align="center")

Remove Default security group and give elb security group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739290136589/98cebd39-ded6-4381-92cc-1d71372a5e76.png align="center")

Give target Group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739290251131/1b600f4d-6668-46d8-a273-f4a631dae73e.png align="center")

<mark>And Create Loadbalancer</mark>

# ✅Result

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739290807685/1d9e860d-9fbf-40f1-888d-171cbae90afc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739290786523/c53f64df-db39-4fd9-8ffa-1c7befdb6b7c.png align="center")

<mark>Let’s build an amazing DevOps &amp; Cloud community together! 💡👩‍💻</mark>

### **<mark>🔗 Connect with Me Everywhere! 🌍</mark>**

📌 **LinkedIn:** [Divya Satpute](https://www.linkedin.com/in/divya-satpute-68666a300/)  
📌 **Instagram (DevOps Content):** [@teacode1122](https://www.instagram.com/teacode1122/)  
📌 **GitHub:** [https://github.com/divyasatpute/vprofile-awsliftshift-project](https://github.com/divyasatpute/vprofile-awsliftshift-project)  
📌 **Hashnode (Technical Blogs):** [https://learnwithdivya.hashnode.dev/](https://learnwithdivya.hashnode.dev/)

📌 **YouTube (Teacode - DevOps Learning):** [https://www.youtube.com/@Teacode-1122](https://www.youtube.com/@Teacode-1122)

💬 Let’s connect, collaborate, and grow together in the **DevOps & Cloud** world! 🚀✨