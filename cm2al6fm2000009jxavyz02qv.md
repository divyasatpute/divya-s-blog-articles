---
title: "Production Level CICD Pipeline Project | CICD DevOps Project"
seoTitle: "CI/CD Pipeline Project for DevOps"
seoDescription: "Learn how to set up a complete CICD pipeline with EKS deployment using Terraform, Jenkins, SonarQube, Nexus, and monitoring tools"
datePublished: Tue Oct 15 2024 15:16:48 GMT+0000 (Coordinated Universal Time)
cuid: cm2al6fm2000009jxavyz02qv
slug: production-level-cicd-pipeline-project-cicd-devops-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1729002307052/29674d4e-e102-417b-8769-c4c0e1aa1f97.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1729005382313/6dbb10b5-e213-47d6-b071-25166a2ff622.jpeg
tags: devops, cicd-cjy1vtdk2005kjjs17n8couc3, devops-articles, tws, teacode

---

What we are doing ????

1. Setup Repo
    
2. Set-Up Required Servers\[Jenkins, SonarQube, Nexus, Monitoring Tools
    
3. Configure Tools
    
4. Create The Pipelines & Create EKS Clusters
    
5. Trigger The Pipeline To Deploy the Application
    
6. Assign a Custom domain to the deployed application
    
7. Monitor The Application
    

# Prerequisites

# Step 1

## Setting up EKS Cluster Using Terraform

AWS Console launch server for terraform

t2 medium

40 storage

open this Ports inbound rule on security group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725537418589/45ed5886-96d3-47a3-8b7b-bc81de1ec0bb.png align="center")

update repo

```bash
sudo apt update -y
```

Install AWS CLI

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
```

AWS Configure Provide Access key and Secret key on Aws Console

```bash
aws configure
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725369408643/73ed7de5-760e-4c17-831c-928d90b728ad.png align="center")

Install Kubectl

```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
```

Installation of Terafform

```bash
sudo snap install terraform --classic
```

```bash
terraform --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725370043785/bf6384c1-e571-45a9-9b67-ea9fedc70cda.png align="center")

clone the Repo for EKS Terraform Script

```bash
git clone https://github.com/divyasatpute/FullStack-Blogging-App.git
```

change directory

```bash
cd FullStack-Blogging-App/
```

change directory

```bash
 cd EKS_Terraform/
```

In Variables.tf file you just need to change Your key name

AND in main.tf file you just need to change region and availability zone as per your requirement

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725370702432/2c7fffcb-f1fa-4240-ab17-e92481d6a640.png align="center")

Now terraform initialization

```bash
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725370909797/a9531d19-cd83-4421-bc03-8c0c9fa9bec4.png align="center")

```bash
terraform plan
```

```bash
terraform apply --auto-approve
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725371760343/8c95fde1-badf-4db5-b857-16cf9ded0ffa.png align="center")

In Order to communicate with aws eks cluster we need to update our kubeconfig file

```bash
aws eks --region ap-south-1 update-kubeconfig --name devopsshack-cluster
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727288258075/e9eaf1a4-16f1-4dea-b28a-78619d9ea4d4.png align="center")

# Step 2

40 GB Storage

Launch 1 EC2 Machine one for Jenkins

t2.large

40 GB storage

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727268472855/72ed201f-ebd9-4710-97f2-0904b662306c.png align="center")

Connect them with using gitbash

# Installation Jenkins

step 1

**Install java ( latest stable version )**

```bash
sudo apt install openjdk-17-jre-headless -y
```

Install Jenkins

```bash
vi 1.sh
```

Paste the all command in 1.sh file

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```

Change the permission

```bash
sudo chmod +x 1.sh
```

Run the file

```bash
./1.sh
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727270362005/ff191c32-3d02-4e46-94ef-61be29f9afc2.png align="center")

## Installation docker on Jenkins machine

Install docker

```bash
sudo apt install docker.io -y
```

change permission

```bash
sudo chmod 666 /var/run/docker.sock
```

## Installation Trivy on Jenkins machine

```bash
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727274142099/47d7df11-a275-4bab-a103-dee5d5240bfa.png align="center")

## Installation kubectl on Jenkins machine

```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
```

## Installation Nexus as a docker container

update machine

```bash
sudo apt update -y
```

Install docker

```bash
sudo apt install docker.io -y
```

Create container

```bash
sudo docker run -d -p 8081:8081 sonatype/nexus3
```

Access your Nexus On Browser **<mark>http://PUBLIC_IP:8081/</mark>**

our Nexus up and running but password is stored inside the container so for that we need to go inside the container

```bash
sudo docker exec -it 629f2dda1a74 /bin/bash
```

```bash
cd sonatype-work/nexus3/
```

```bash
cat admin.password
```

here you can got password

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725373556066/32e8c428-9727-41b2-b83c-93221d839390.png align="center")

Now You Can See Our Nexus also working fine and able to sign in

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727270408882/1d132321-787c-47ad-973b-c80da46c607d.png align="center")

### Nexus Configuration

Go to nexus dashboard --&gt; click on settings ---&gt; click on repositories

copy the Maven-releases URL and Maven snapshot URL and paste it on POX.XML file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725389263954/4a32ce76-9b01-430b-ad2d-f09e070f055c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725389406005/d2cc5d59-ad6a-463c-b83a-c335d33d23ce.png align="center")

for credentials go to Jenkins Dashboard ---&gt;click on manage Jenkins---&gt; Managed files---&gt; click on Add new Config---&gt;Global Maven settings.xml---&gt;provide id "anything"---&gt; click on next

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725390156594/72abc1cd-1276-48e4-bdb7-7ce76c177357.png align="center")

## Installation SonarQube as a docker container

update machine

```bash
sudo apt update -y
```

Install docker

```bash
sudo apt install docker.io -y
```

Create container

```bash
sudo docker run -it -p 9000:9000 sonarqube:lts-community
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727271144521/1d4bf569-d041-4fbf-a331-10092f1a49e8.png align="center")

## Configuration on Jenkins

# Installation Plugins

**SonarQube Scanner**

**Config File Provider**

**Maven Integration**

**Pipeline Maven Integration**

**Kubernetes**

**Kubernetes Client API**

**Kubernetes Credentials**

**Kubernetes CLI**

**Kubernetes Credentials Provider**

**Docker Pipeline**

**Docker Commons**

**Docker**

**Eclipse Temurin installer**

**Pipeline: Stage View**

### **Configuration System**

Sonar Scanner

### **Configuration tools**

Go to Manage jenkins ----&gt; tools

add SonarQube Scanner

add Maven

Add Docker

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727272832216/bd8fa61a-407b-4300-bfcb-cccb43a819e1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727272868868/f75b11ac-ff83-4b8e-826f-354b96241801.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727272900289/ec43936c-5bca-4b79-95a4-1a4d3113b222.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727273057326/903fe4c9-9359-4650-af01-068168478311.png align="center")

### <mark>Deployment</mark>

## Create Service Account, Role & Assign that role, And create a secret for Service Account and generate a Token

### Create namespace

```bash
kubectl create ns webapps
```

### Creating Service Account

```bash
vi svc.yml
```

```bash
apiVersion: v1
kind: ServiceAccount
metadata:
  name: jenkins
  namespace: webapps
```

```bash
kubectl apply -f svc.yml
```

### Create Role

```bash
vi role.yml
```

```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: app-role
  namespace: webapps
rules:
  - apiGroups:
        - ""
        - apps
        - autoscaling
        - batch
        - extensions
        - policy
        - rbac.authorization.k8s.io
    resources:
      - pods
      - componentstatuses
      - configmaps
      - daemonsets
      - deployments
      - events
      - endpoints
      - horizontalpodautoscalers
      - ingress
      - jobs
      - limitranges
      - namespaces
      - nodes
      - secrets
      - pods
      - persistentvolumes
      - persistentvolumeclaims
      - resourcequotas
      - replicasets
      - replicationcontrollers
      - serviceaccounts
      - services
    verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
```

```bash
kubectl apply -f role.yml
```

### Bind the role to service account

```bash
 vi bind.yml
```

```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: app-rolebinding
  namespace: webapps 
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: app-role 
subjects:
- namespace: webapps 
  kind: ServiceAccount
  name: jenkins
```

```bash
kubectl apply -f bind.yml
```

for token

```bash
vi jen.secret.yml
```

```bash
apiVersion: v1
kind: Secret
type: kubernetes.io/service-account-token
metadata:
  name: mysecretname
  annotations:
    kubernetes.io/service-account.name: jenkins
```

```bash
kubectl apply -f jen.secret.yml -n webapps
```

for docker secret

```bash
kubectl create secret docker-registry regcred \
    --docker-server=https://index.docker.io/v1/ \
    --docker-username=divyasatpute \
    --docker-password=123654 \
    --namespace=webapps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727289964553/9e455c32-88b8-4216-8da8-d4bc6d461ddf.png align="center")

```bash
kubectl describe secrets mysecretname -n webapps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727290110320/a022455b-4acb-4d53-a16a-4ec59eec3113.png align="center")

# Pipeline

```bash
pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/divyasatpute/full-stack-app-project.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Trivy fs scan') {
            steps {
                sh 'trivy fs --format table -o fs.html .'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Blogging-app -Dsonar.projectKey=Blogging-app \
                 -Dsonar.java.binaries=target'''
               }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Publish Artifacts') {
            steps {
               withMaven(globalMavenSettingsConfig: 'maven-settings', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                 sh 'mvn deploy'
                }
            }
        }
         stage('Docker Build & Tag ') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                    
                sh 'docker build -t divyasatpute/bloggingapp:latest . --no-cache '
                   }
                }
            }
        }
        stage('Trivy image scan') {
            steps {
                sh 'trivy image --format table -o image.html divyasatpute/bloggingapp:latest'
            }
        }
        stage('Docker Push') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                    
                sh 'docker push divyasatpute/bloggingapp:latest'
                   }
                }
            }
        }
        stage('k8-Deploy') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'devopsshack-cluster', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://0D7DFCF662ECC24043497267C6A5BDEB.gr7.ap-south-1.eks.amazonaws.com') {
                sh 'kubectl apply -f deployment-service.yml'
                sleep 20
                }
            }
        }
         stage('verify the Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'devopsshack-cluster', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://0D7DFCF662ECC24043497267C6A5BDEB.gr7.ap-south-1.eks.amazonaws.com') {
                sh 'kubectl get pods'
                sh 'kubectl get svc'
                }
            }
        }
        
    }
}
```

## Installation Monitaring tool

```bash
sudo apt update -y
```

```bash
wget https://github.com/prometheus/prometheus/releases/download/v3.0.0-beta.0/prometheus-3.0.0-beta.0.linux-amd64.tar.gz
```

```bash
tar -xvf prometheus-3.0.0-beta.0.linux-amd64.tar.gz
```

```bash
wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.25.0/blackbox_exporter-0.25.0.linux-amd64.tar.gz
```

```bash
tar -xvf blackbox_exporter-0.25.0.linux-amd64.tar.gz
```

```bash
cd prometheus-3.0.0-beta.0.linux-amd64
```

```bash
./prometheus &
```

```bash
cd prometheus-3.0.0-beta.0.linux-amd64
```

```bash
vi prometheus.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727353602051/e89fe2c7-9777-4e73-abd6-4ca64b8b2a71.png align="center")

> access prometheus [http://13.232.13.30:](http://13.232.13.30:9090/query)<mark>9090</mark>

for blackbox exporter

```bash
cd blackbox_exporter-0.25.0.linux-amd64
```

```bash
./blackbox_exporter &
```

access blackbox [http://13.232.13.30:](http://13.232.13.30:9090/query)<mark>9090</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727353058004/6dbccf80-5223-4c59-b27b-1b38e257bad4.png align="center")

### for Grafana

```bash
sudo apt-get install -y adduser libfontconfig1 musl
```

```bash
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_11.2.0_amd64.deb
```

```bash
sudo dpkg -i grafana-enterprise_11.2.0_amd64.deb
```

```bash
sudo /bin/systemctl start grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727352512353/fe750103-1b58-4e62-baae-da11cc71c64e.png align="center")

## <mark>Test Results</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727279017024/4980789b-aafd-41b6-a3c9-1bd1ad8e9ad0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727280553770/92fbe6f6-a467-4638-a83c-48f64f5733e5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727347277881/f0d0538f-1a80-44af-b51a-3c99519268bf.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727351821671/4557af16-46ba-437c-9747-714f74700327.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727361329567/13e7986c-1c7a-492d-b9bb-18239f19322c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727361806636/c704f14a-8834-45a2-8946-d48bd75ac5f8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727362123452/8c175418-083b-4db2-a599-dde3752e016f.png align="center")