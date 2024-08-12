---
title: "Jenkins on Server Push Based Approach CICD"
seoTitle: "Jenkins Push-Based CICD Approach Project"
seoDescription: "Guide on Jenkins setup for CI/CD: server push, SSL, NGINX reverse proxy, Docker, and Helm integration"
datePublished: Mon Aug 12 2024 10:21:44 GMT+0000 (Coordinated Universal Time)
cuid: clzquggf5001v08l1hyh38co0
slug: jenkins-on-server-push-based-approach-cicd
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723451386373/26907492-f70b-407a-9c41-bfa5543fd4f6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723458028241/293b5a3c-2eb4-4d90-ab43-ff4fcce24241.png
tags: projects, devops, cicd, devops-articles, iw, tws, diu

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723314955662/f2acad88-0354-49fb-a5f1-370c82d1b7a4.png align="center")

* **What is <mark>CI/CD?</mark>** 🛠️
    
    * Continuous Integration (CI) + Continuous Deployment (CD).
        
    * Automates software delivery process.
        
* **Server Push Based Approach** 🔄
    
    * Code changes are automatically pushed to the server.
        
    * Reduces manual intervention and accelerates deployment.
        
* **<mark>Jenkins Overview</mark>** <mark>🐱‍👤</mark>
    
    * Popular open-source automation server.
        
    * Supports building, deploying, and automating projects.
        
* **How It Works** 🖥️
    
    * **Code Push**: Developers push code to a version control system (e.g., Git) 🌐.
        
    * **Webhook Trigger**: A webhook notifies Jenkins of changes 🔔.
        
    * **Build Process**: Jenkins pulls the latest code and runs builds/tests 📊.
        
    * **Deployment**: Successful builds are automatically deployed to the server 🚢.
        
* **<mark>Benefits</mark>** <mark>✅</mark>
    
    * **Faster Feedback**: Immediate results on code changes.
        
    * **Automated Testing**: Ensures code quality through automated tests 🧪.
        
    * **Consistent Releases**: Reduces human error in deployments.
        
    * **Scalability**: Easily integrates with other tools and systems 🔗.
        
* **<mark>Common Tools Used</mark>** <mark> 🔧</mark>
    
    * **Version Control**: Git
        
    * **Notification Services**: Slack, email alerts.
        
    * **Containerization**: Docker for consistent environments 🐳.
        
* **<mark>Use Cases</mark>** <mark> 📌</mark>
    
    * Agile development teams looking for rapid iterations.
        
    * Organizations aiming for DevOps practices to improve collaboration.
        

# Step by Step guide

### Prerequisites

you must have your purchase domain and create hosted zone in Route 53 and replace this namespaces with your domain

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723308279434/0691061b-6459-4bff-930b-a0eb2909a271.png align="center")

### Git clone

```bash
git clone https://github.com/divyasatpute/Jenkins.git
```

push this repo on your github

```bash
git push <your github repo URL >
```

### Create Cluster using kubeadm script (step1)

For that you need to create 4 machine cluster

In this POC we need 1 **master** and 2 **worker** machine and **Jenkins** machine separately

**On AWS Console**

* 4 EC2 machine
    
* ubuntu 20.04 AMI
    
* volume 40GB (storage)
    
* c5.xlarge Machine Type
    

after you have to connect all on gitbash

And update all cluster using following command :

```bash
sudo apt update -y
```

And set hostname for each node

```bash
sudo hostname Master
sudo hostname Worker1
sudo hostname Worker2
```

Come on root user

```bash
sudo -i
```

now on master node paste the following command (EKS Script ) Controlplane script

```bash
bash <(curl -s https://raw.githubusercontent.com/isakibshaikh1/Kubeadm/main/kubeadm/master.sh)
```

And on another on both Worker node paste following command (worker script)

```bash
bash <(curl -s https://raw.githubusercontent.com/isakibshaikh1/Kubeadm/main/kubeadm/worker.sh)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721312741379/11c71460-b2e1-4fca-a97c-67111f6d0e66.jpeg align="center")

> now your master node is ready take this token from master node and paste on worker node for join worker node to master

```bash
kubeadm join 172.31.46.89:6443 --token qanxgm.tmberexbyo3n0dpr --discovery-token-ca-cert-hash sha256:c2b6ac5e46556ed69c940fa8725eb37e6ccbeaa3f39117fc71a481a1798eac3c
```

as you can see node will be ready but worker node yet not ready state

##### Note that both nodes are NotReady. This is OK because we have not yet installed networking.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723047690483/85508aa8-92cf-4b7a-aed8-d9d33567574b.png align="center")

for that we have use some plugins **Install a Network Plugin**

##### Doc Ref : [Installing Network Plugin Addons](https://kubernetes.io/docs/concepts/cluster-administration/addons/)

Install Weave Net [: Weave Net](https://www.weave.works/docs/net/latest/kubernetes/kube-addon/)

```python
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723048088452/64d0028e-e3ad-4575-89e1-5f1062fae2ae.png align="center")

### Installation of Jenkins (step 2)

\### **<mark>How to deploy Jenkins with Our custom domain and SSL</mark>** ###

For install Jenkins we need to follow below shell script, i am using ubuntu 20.04 this script also work for ubuntu 22.04

```bash
vi jenkins.sh
```

Paste this script in Jenkins.sh

```bash
#! /bin/bash

sudo apt update
sudo apt install openjdk-11-jre -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt install -y maven
sudo apt-get install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

Run script using this command

```bash
sh jenkins.sh
```

After that we need to check using Jenkins using ec2 instance id for example:- **<mark>34.203.34.186:8080</mark>** for checking purpose but our end goal its should not be run on this after configuring nginx reverse proxy will be remove port 8080 from ec2 instance security group and check , **Here you can see our Jenkins up and running**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723049476312/cdeb6d41-9405-4d3a-aa7f-35a576dbf86c.png align="center")

Access your Jenkins Dashboard on browser now

> Note: Make sure you enable 8080 port in Security Group Inbound Rules.
> 
> Get the initial administration password
> 
> $sudo cat /var/lib/jenkins/secrets/initialAdminPassword

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720175911910/f3b5cf23-23f7-4bce-97e3-72e00373564b.jpeg align="center")

**Now your Jenkins started : <mark>Create Admin user</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720175954747/e82cbef6-f72e-455c-a03d-2d04b8ad3a36.jpeg align="center")

**🎉Now , appreciate yourself you successfully deploy Jenkins on your machine 🎉**

it is Look like this **: <mark>Jenkins up and Running but this is not yet secured we have to add SSL for secure connection</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723050023330/9d3b4d64-cd26-40d1-8824-ad2186c58cc6.png align="center")

---

### Step-by-step guide to configure SSL on Jenkins using Let's Encrypt and NGINX reverse proxy (step 3)

1. Install NGINX on your server if it's not already installed. You can do this by running the following command:
    
    ```bash
    #update repository first 
    sudo apt-get update -y
    #install nginx by following commad
    sudo apt-get install nginx -y
    #check nginx status 
    sudo systemctl status nginx
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723050402658/902a1602-12a4-44ce-b82c-fc210a2104d4.png align="center")
    
2. Create a new server block configuration file for Jenkins. You can do this by creating a new file in the /etc/nginx/sites-available/ directory. For example:
    
    ```bash
    sudo vi /etc/nginx/sites-available/jenkins
    ```
    
3. Add the following content to the file: Note: <mark>Replace </mark> [<mark>jenkins.example.com</mark>](http://jenkins.example.com) <mark>with your Jenkins domain name.</mark>
    
    ```bash
    server {
        listen 80;
        server_name jenkins.learnwithdivya.online;
    
        location / {
            proxy_pass http://localhost:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;        
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
    ```
    
4. Create a symbolic link to the server block configuration file in the /etc/nginx/sites-enabled/ directory:
    

```bash
sudo ln -s /etc/nginx/sites-available/jenkins /etc/nginx/sites-enabled/
```

> Note: you can see /etc/nginx/sites-available/jenkins on this path the file - represented simple file ( $sudo ls -lrt /etc/nginx/sites-available/jenkins)
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723052097566/e9b9a43b-c007-4155-880b-acf89979010d.png align="center")
> 
> after running above command its create shortcut because by default Jenkins look this file on /etc/nginx/sites-enabled location (ls -lrt /etc/nginx/sites-enabled)
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723052334249/b6524a62-3d56-4ed3-a8a0-7c23507655d5.png align="center")

5. Test the NGINX configuration and restart the NGINX service:
    
    ```bash
    sudo nginx -t
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723055390279/8e60bc0f-f045-42b4-9d8f-67196b16e9cb.png align="center")
    

```bash
#restart the nginx server
sudo systemctl restart nginx
```

6. Install Certbot, the Let's Encrypt client, by running the following commands:
    
    ```bash
    sudo apt-get update -y
    
    sudo apt-get install certbot python3-certbot-nginx -y
    ```
    
7. Obtain an SSL certificate for your Jenkins domain name using Certbot:
    

```bash
sudo certbot --nginx -d jenkins.learnwithdivya.online
#Note:Replace jenkins.example.com with your Jenkins domain name.
```

8. After running above you can found error like this :
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723056434021/6960da68-40e8-4bad-b7cc-918f28c9dee6.png align="center")

For resolve this issue you need to create A name record on your Route53 service

Go to route53 --&gt; click on hosted zone --&gt; click on your domain name ---&gt; create on record , once it will be insync then you can try again above command

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723056953889/5bd7d2f0-90ad-4fee-b576-ed07151cd7b0.png align="center")

🎉 **Congratulations!** 🎉

You've put in hard work, dedication, and perseverance to reach this milestone!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723057170041/df049643-6294-4252-bc31-e09297fe9e47.png align="center")

Now your Jenkins runs in secure with <mark>SSL certificate</mark> in <mark>secure site</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723057426005/5e860de8-b0a4-484c-a7b4-c69e5d1e15fc.png align="center")

> It means without using LLB we are use nginx as a reverse proxy : if you are trying to click http:// still it will be redirect to https://
> 
> Sounds interesting, right?

Now move to next

### create <mark>webhook</mark> on Github(step 4)

* Click on repo settings ---&gt;
    
* click on webhook ----&gt;
    
* Add new Webhook ---&gt;
    
* in Playload URL configure your Jenkins URL followed by github-webhook and content type json
    
* click on ADD webhook
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723058810103/935727a5-2c9f-4891-963d-0763f2d5b94a.png align="center")
    

**Our Webhooks are ready**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723221368691/6300ccd8-4fdc-4420-89fd-bb2c8de4b98a.png align="center")

### 🐳Docker Install on Jenkins machine🐳

```bash
sudo apt install docker.io -y
```

Give permission to socket

```bash
 sudo usermod -aG docker $USER
 sudo chown $USER:docker /var/run/docker.sock
```

change ownership

```bash
sudo chown jenkins:docker /var/run/docker.sock
```

Go to docker hub account generate token

now on your Jenkins machine click on **manage Jenkins** --&gt; click on [**Credentials**](https://jenkins.learnwithdivya.online/manage/credentials/) **\---&gt;**

**system ---&gt; global** [**Credentials**](https://jenkins.learnwithdivya.online/manage/credentials/)

**ADD your docker token as a password**

**ADD (ID) which is you given in your pipeline**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723449778520/676570f1-63d6-45f3-99c5-04b48c2208c6.png align="center")

### Plugins Installation

Manage Jenkins --&gt; plugins ---&gt; available plugins ----&gt;

1. docker
    
2. docker Pipeline
    
3. docker commons
    
4. docker -build-steps
    
5. docker slave
    

**install it**

### Installation of Helm

**Helm Install on <mark>Jenkins</mark> Machine and <mark>Master Node</mark>**

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

configuration on master node

change directory

```bash
 cd .kube/
```

copy config file in /home/ubuntu

change directory

```bash
cd /home/ubuntu/
```

change ownership

```bash
sudo chown ubuntu:ubuntu config
```

break connection come into your local machine download folder

```bash
exit
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723299612269/232debf0-4138-4c02-9003-7fa4969a6ffc.png align="center")

Now fire this command on local **(copy file from remote to local)**

```bash
scp -i divya.pem ubuntu@43.204.109.240:/home/ubuntu/config .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723299838513/bdf0c908-483f-492f-9d61-de3545b74cec.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723299938825/2662891c-c90c-405f-92e1-b675d63f9fca.png align="center")

New to go to Jenkins dashboard

1. click on manage Jenkins
    
2. click on Credencials
    
3. select as a secrete file
    
4. and upload config file
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723304202644/ed232563-cd18-4e9b-8f13-c72ede15b836.png align="center")

* Go to Jenkins dashboard
    
* click on manage Jenkins
    
* click on available plugins
    

1. [**Kubernetes Client API**](https://plugins.jenkins.io/kubernetes-client-api)
    
2. [**Kubernetes Credentials**](https://plugins.jenkins.io/kubernetes-credentials)
    
3. [**Kubernetes**](https://plugins.jenkins.io/kubernetes)
    
4. [**Kubernetes CLI**](https://plugins.jenkins.io/kubernetes-cli)
    
5. [**Kubernetes Credentials Provider**](https://plugins.jenkins.io/kubernetes-credentials-provider)
    

* **install it**
    

\### How to Set Up the Jenkins + GitHub Integration ###

**NOW LAST STEP TO ACHIEVE THE THINGS**

create Jenkins pipeline

```bash
pipeline {
    agent any
    stages {
        stage('Build Maven') {
            steps {
                sh 'pwd'
                sh 'mvn clean install package'
            }
        }

        stage ('Copy Artifacts') {
            steps {
                sh 'pwd'
                sh 'cp -r target/*.jar docker'
            }
        }    

        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Docker Image'){
            steps{
                script {
                    def customImage = docker.build("iamsakib/petclinic:${env.BUILD_NUMBER}", "./docker")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    customImage.push()    
                }
            }
        }
    }

        stage('Build on kubernetes'){
        steps {
            withKubeConfig([credentialsId: 'kubeconfig']) {
                sh 'pwd'
                sh 'cp -R helm/* .'
                sh 'ls -ltrh'
                sh 'pwd'
                sh '/usr/local/bin/helm upgrade --install petclinic-app petclinic --set image.repository=iamsakib/petclinic --set image.tag=${BUILD_NUMBER}'
        }
    }
}



}

}

#replace yours id
```

### Deployment of Application

Go to Jenkins dashboard

click on new item

give name to your project

select pipeline

select GitHub hook trigger for GITScm polling

select pipeline script with SCM

SCM =git and configure GIT URL and branch

script path should be jenkinsfile (jenkinsfile should be available on your git repo)

save and apply

Access your application &lt;**<mark>worker_node_Pliblic_IP:32740</mark>**\&gt;

And boommmmmmmmmmmmm

### 🌟 **Way to Go!** 🌟

You've done it—what an incredible achievement! This moment is a testament to your effort, resilience, and talent. You faced the challenge head-on and came out on top, and now it's time to celebrate that success.

Remember, this is proof of what you're capable of. Keep pushing forward, and don't forget to enjoy every victory along the way. You've earned it—**congratulations!**

### ✅Test Results ✅

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723305811124/302df26c-729f-466e-9274-29a9f471c9ea.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723062320703/be6b4d18-47c6-4dd6-9202-a08d13c0627c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723305933196/27b2a63a-4aed-488a-9180-7a5c5b1a5a22.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723306483775/176062d3-4fa1-4cd4-8580-4805dd2fe045.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723307720290/7869d2db-596d-4dac-ae7a-bb3e5a2f83e3.png align="center")