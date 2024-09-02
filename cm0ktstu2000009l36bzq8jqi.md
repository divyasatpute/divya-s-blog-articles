---
title: "🚀11 Microservice CICD Pipeline DevOps Project | Ultimate DevOps Pipeline🚀"
seoTitle: "Microservice CICD DevOps Pipeline Project"
seoDescription: "Guide to creating a microservices CICD pipeline with Jenkins, Docker, and Kubernetes for scalable, flexible, and resilient apps. 🌟🚀"
datePublished: Mon Sep 02 2024 09:56:27 GMT+0000 (Coordinated Universal Time)
cuid: cm0ktstu2000009l36bzq8jqi
slug: 11-microservice-cicd-pipeline-devops-project-ultimate-devops-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1725270633857/e326827f-9dd6-4c6d-894b-0161c761dec2.gif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1725270953623/792f9286-b3d1-4b37-b762-a534c70341ea.gif
tags: microservices, stackoverflow, docker, aws, projects, jenkins

---

Embarking on a microservices project can be an exciting journey, filled with opportunities to create scalable, flexible, and resilient applications. Here’s a comprehensive, step-by-step guide to help you navigate this architectural paradigm and build a successful microservices-based application. Let’s dive in! 🌟

### Prerequisites

**First Create a user in AWS IAM with any name**

**Attach Policies to the newly created user**

1. AmazonEC2FullAccess
    
2. AmazonEKS\_CNI\_Policy
    
3. AmazonEKSClusterPolicy
    
4. AmazonEKSWorkerNodePolicy
    
5. AWSCloudFormationFullAccess
    
6. IAMFullAccess
    
7. One more policy we need to create with content as below
    
    ```plaintext
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": "eks:*",
                "Resource": "*"
            }
        ]
    }
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725192333097/65519488-bc89-47a9-a49d-f2b493d55613.png align="center")
    

**Create EC2 machine with t3medium**

update the repo

```bash
sudo apt update -y
```

Make directory

```bash
mkdir script
```

change directory

```bash
cd script
```

make file

```bash
sudo vi 1.sh
```

paste it below commands in this file which install AWS CLI , KUBECTL, EKSCTL

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

Give permission for Excuteble mode

```bash
sudo chmod +x 1.sh
```

Run the script

```bash
sudo ./1.sh
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725195018805/6d05c798-e6a8-43f0-89b7-20b95be7086b.png align="center")

configure aws (give access key and secrete key which is you generate on aws console

```bash
aws configure
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725195146506/9337c643-9998-4a55-bb5b-915cfe135b96.png align="center")

### Now create EKS cluster

```bash
eksctl create cluster --name=EKS-1 \
                      --region=ap-south-1 \
                      --zones=ap-south-1a,ap-south-1b \
                      --without-nodegroup
#make sure you change region as per your region
```

Provide oidc provider

```bash
eksctl utils associate-iam-oidc-provider \
    --region ap-south-1 \
    --cluster EKS-1 \
    --approve
```

create node (replace your public key name and region and configure as per your requirement )

```bash
eksctl create nodegroup --cluster=EKS-1 \
                       --region=ap-south-1 \
                       --name=node2 \
                       --node-type=t3.medium \
                       --nodes=3 \
                       --nodes-min=2 \
                       --nodes-max=4 \
                       --node-volume-size=20 \
                       --ssh-access \
                       --ssh-public-key=DevOps \
                       --managed \
                       --asg-access \
                       --external-dns-access \
                       --full-ecr-access \
                       --appmesh-access \
                       --alb-ingress-access
```

> Note : Open INBOUND TRAFFIC IN ADDITIONAL Security Group

Now our cluster is ready hurrayyyy

### Installation of Jenkins

### Prerequisites:

java 17 version installed

```bash
sudo vi jenkins.sh
```

Paste it in file below content

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

Give permission to jenkins.sh file

```bash
sudo chmod +x jenkins.sh
```

Run the script

```bash
sudo ./jenkins.sh
```

Access your Jenkins on Browser **http://publicIP:8080/**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725197074083/b9053880-66f7-433c-9830-0a7d00e348ba.png align="center")

### Installation Docker

```bash
 sudo apt  install docker.io -y
```

Give permission to Docker socket

```bash
 sudo chmod 666 /var/run/docker.sock
```

### Installation plugins on Jenkins Dashboard

**<mark>For Docker</mark>**

Manage Jenkins ---&gt; plugins ---&gt; Available plugins

* Docker
    
* Docker pipeline
    
* Docker Commons
    
* Docker slaves
    
* Docker build step
    

**<mark>For Kubernetes</mark>**

* Kubernetes
    
* Kubernetes CLI
    
* Kubernetes API
    
* Kubernetes Credentials Provider
    

**<mark>for scanning</mark>**

* Multibranch Scan Webhook Trigger
    

Installation of Tools on Jenkins dashboard

Manage Jenkins ---&gt;Global tools ---&gt; docker installation

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725198059023/db5b0b98-709b-4374-ad48-c24698164c7e.png align="center")

### Credentials

Manage Jenkins---&gt; Credentials----&gt; Global Credentials

add token as a password for docker and also for github

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725198974271/40862dea-4e4c-425d-801f-064a25205bb9.png align="center")

## Create Multibranch Pipeline

* Go to New Item
    
* give name of project
    
* Select Multibranch pipeline
    
* select Branch Source (Git)
    
* select **Scan Multibranch Pipeline Triggers**
    
* select Scan by webhook and add token
    

### Create Webhook

Go to github repo ----&gt;settings

select webhhok

add this two configuration make sure replace your information

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725208257780/d6ad0c80-30ee-4db3-aea4-6bb2861ea73c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725208319032/0593002b-f1ee-4b79-8a8e-7ce53d90ce4d.png align="center")

once you trigger the webhook its automatically job done

### <mark>Deployment</mark>

Create namespace

```bash
kubectl create namespace webaaps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725212517400/74551c90-575a-4744-99f5-59c2043d21bc.png align="center")

we have to create service account

```bash
sudo vi svc.yml
```

```bash
apiVersion: v1
kind: ServiceAccount
metadata:
  name: jenkins
  namespace: webapps
```

create this by run this command

```bash
 kubectl apply -f svc.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725212799310/e930428f-b7e7-44cd-befa-7ca5d220c148.png align="center")

create role for this service

```bash
vi role.yml
```

```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: app-role
  namespace: webaaps 
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

Create this by following command

```bash
kubectl apply -f role.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725213041110/b6dc1be9-c9ab-40e3-bf6a-f20633533eee.png align="center")

now bind it

```bash
sudo vi bind.yml
```

```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: app-rolebinding
  namespace: webaaps 
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: app-role 
subjects:
- namespace: webaaps 
  kind: ServiceAccount
  name: jenkins
```

Run this

```bash
kubectl apply -f bind.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725213252088/4c88d889-f794-49c4-9c17-0d57d58dfae8.png align="center")

### Generate token using service account in the namespace

```bash
sudo vi sec.yml
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

create this by following command

```bash
 kubectl apply -f sec.yml -n webaaps
```

we want token now display token by following command

```bash
kubectl describe secret mysecretname -n webaaps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725214179538/e636d891-45b1-436d-a395-5cb8ec912f2e.png align="center")

add this above token as a k8 creadentials

write deployment jenkinsfile replace this with your cluster information

```bash
pipeline {
    agent any

    stages {
        stage('Deploy Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName: 'EKS-1',
                    contextName: '',
                    credentialsId: 'k8-token',
                    namespace: 'webaaps',
                    serverUrl: 'https://FACF5859BB7FEC1D667A82242A1A14E0.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName: 'EKS-1',
                    contextName: '',
                    credentialsId: 'k8-token',
                    namespace: 'webaaps',
                    serverUrl: 'https://FACF5859BB7FEC1D667A82242A1A14E0.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh "kubectl get svc -n webaaps"
                }
            }
        }
    }
}
```

Acesss your application by this url : [http://a997381f85bc940abab29a1fb772ea1e-13101926.ap-south-1.elb.amazonaws.com/](http://a997381f85bc940abab29a1fb772ea1e-13101926.ap-south-1.elb.amazonaws.com/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725215795360/49937603-cc21-4a69-851f-5658d3b445d8.png align="center")

## <mark>Test Result</mark>

### <mark>Build Success</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725215904410/5743becf-1f0a-46da-96fe-e1d76722a4a2.png align="center")

### <mark>Github repo</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725217486797/48416345-c455-4c4a-b56c-f735ae4554a5.png align="center")

### <mark>Cluster created successfully</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725217591779/49cb0cce-120d-492f-aa55-2490628e0f54.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725217647242/1578b725-e1bf-4d07-8741-ca42521c0924.png align="center")

### <mark>Docker hub</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725215967946/71affd95-325a-4273-a839-9c911541419d.png align="center")

### <mark>Final URL</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725215795360/49937603-cc21-4a69-851f-5658d3b445d8.png align="center")

## <mark>Application</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725216101510/e7b65a9f-f6fd-4663-a86d-3c0d5ed86f43.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725216158245/8752b097-5559-424b-b33e-0c0fa659c06f.png align="center")

#### **Conclusion 🌟**

Building a microservices-based application is a rewarding endeavor that brings flexibility, scalability, and resilience to your software architecture. By following this step-by-step guide, you can navigate the complexities of microservices and create a robust application tailored to meet your needs. Happy building! 🚀💻

If you're looking to get a better grasp on Kubernetes deployments, you might find this video super helpful: [Check it out here!](https://youtu.be/SO3XIJCtmNs?si=-vsfESyApji-ee8o) [🎥✨](https://youtu.be/SO3XIJCtmNs?si=-vsfESyApji-ee8o)

%[https://youtu.be/SO3XIJCtmNs?si=-vsfESyApji-ee8o] 

It’s packed with useful info and clear examples that can make everything click! Let me know if you have any questions or if there's anything else I can help with. 😊