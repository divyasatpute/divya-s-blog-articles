---
title: "Docker to Kubernetes Migration MEGA PROJECT"
seoTitle: "Docker to Kubernetes Migration Guide"
seoDescription: "Guide to migrating from Docker to Kubernetes, covering architectures, components, and project hands-on steps"
datePublished: Tue Aug 27 2024 15:35:32 GMT+0000 (Coordinated Universal Time)
cuid: cm0cl9seo000009jph7ew3x30
slug: docker-to-kubernetes-migration-mega-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724772526053/80b1b4a0-a690-4152-82e7-667417cd39d2.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724772744646/6adf26ec-be49-40e1-abb2-515798dbb2d1.jpeg
tags: docker, kubernetes, migration, devops, devops-articles, diu

---

## TOPICS COVERED

1. Docker Architecture
    
2. Kubernetes Architecture
    
3. Docker to kubernetes Migration
    
4. Kubernetes Components
    
5. K8 ConfigMaps
    
6. K8 Persistent Volumes
    
7. K8 Secrets
    
8. K8 Deployments
    
9. K8 Service
    
10. Namespace
    
11. Database deployments
    
12. K8 Persistent Volumes Claims
    

## Docker Architecture

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724667266541/5c4ec456-52e7-42e4-8039-68fe88e4f644.png align="center")

## Kubernetes Architecture

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724667379044/a670325e-bf70-4e83-90bd-07e8bab61b44.png align="center")

### Cluster Architecture

A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes, that run containerized applications. Every cluster needs at least one worker node in order to run Pods.

**Control plane components**

**<mark>1) Kube-apiserver </mark>** The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.

**<mark>2) Etcd </mark>** Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

**<mark>3) kube-scheduler</mark>** Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

**<mark>4) kube-controller-manager</mark>**

There are many different types of controllers. Some examples of them are:

● Node controller: Responsible for noticing and responding when nodes go down.

● Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.

● EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).

● ServiceAccount controller: Create default ServiceAccounts for new namespaces.

### Node components

A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes, that run containerized applications. Every cluster needs at least one worker node in order to run Pods.

**<mark>Control plane components</mark>**

**<mark>1) kubelet</mark>**: An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.The kubeket takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. The kubelet doesn't manage containers which were not created by Kubernetes.

**<mark>2) kube-proxy</mark>** : kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.

**<mark>3) Container runtime</mark>** : A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment.

**<mark>4) Pods</mark>**

## Docker to kubernetes Migration

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724667894900/5f86a884-9c9e-4e2a-a1b8-f8676dcf9bac.png align="center")

## Why Move from Docker Compose to Kubernetes

### Single-cluster limitation of Compose

Docker Compose containers run on a single host. When multiple hosts or cloud providers are used to run an application workload, this presents a network communication challenge. Using Kubernetes, you can manage multiple clusters and clouds more easily.

### Single point of failure in Compose

Docker Compose-based applications require that the server running the application be kept running for them to continue working. This leads to a single point of failure on the server running Compose. Contrary to this, Kubernetes runs typically in a highly available (HA) state with multiple servers deploying and maintaining the applications. The nodes are also scaled based on resource utilization in Kubernetes.

### The extensibility of Kubernetes

Platforms like Kubernetes are highly extensible, which is why they are popular with developers. Pods, Deployments, ConfigMaps, Secrets, and Jobs are some native resource definitions. Clustered applications run using each of them for different purposes. The Kubernetes API server provides the ability to use CustomResourceDefinition to add custom resources.

### open source support of Kubernetes

Kubernetes is a powerful platform that continues to grow rapidly among enterprises. Over the past two years, it has ranked among the most popular platforms and the most desired among software developers. It stands out among container orchestration and management tools.

## K8 Deployments / Services

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 3
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724668165314/58f13b63-e7d3-4c3b-b6dc-81e2d209decf.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724668285658/2c4e796e-911a-46a9-9b37-cdc25c747cdf.png align="center")

## K8 ConfigMaps

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724668379440/500268a4-c1dc-472b-889c-42c65b643b18.png align="center")

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724668478442/f2d965d9-961d-4670-844e-a45e7d3860c1.png align="center")

## K8 Secrets

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.

```bash
apiVersion: v1
kind: Secret
metadata:
name: secret-basic-auth
type: kubernetes. io/basic-auth
stringData:
username: admin # required field for kubernetes.io/basic-auth
password: t0p-Secret # required field for kubernetes.io/basic-auth
```

```bash
apiVersion: v1
kind: Secret
metadata:
name: secret-sa-sample
annotations:
kubernetes.io/service-account.name: "sa-name"
type: kubernetes. io/service-account-token
data:
extra: YmFyCg ==
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724668688756/cb020d37-9323-4ea4-bb3d-8b8b0db9df3d.png align="center")

## PV & PVC in Kubernetes

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724668743668/22d149fb-5314-4faa-9057-4b297e87e59d.png align="center")

The main difference between PV and PVC is that PV represents a piece of storage in a cluster, while PVC represents a request for storage by a pod

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724668869521/0636ad89-6b45-4c1a-b738-fca3a6b7c823.png align="center")

## KUBERNETES PROJECT HANDSON

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724669018805/27830641-896b-4373-9d6a-704fbaf30fc2.png align="center")

### Now here we started our main project Handson

**<mark>STEP 1</mark>**

TAKE THE LINUX2 AMI EC2 WITH 20 GB AND T2.MEDIUM

**<mark>STEP 2</mark>**

Fire below command on terminal

```bash
sudo yum update -y
```

```bash
sudo yum install docker -y
```

```bash
sudo systemctl start docker
```

```bash
sudo systemctl enable docker
```

```bash
sudo yum install conntrack -y
```

```bash
sudo yum install git -y
```

**<mark>STEP 3</mark>**

\- Download Minikube

```bash
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

**<mark>STEP 4 -</mark>**

```bash
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

```bash
sudo chmod 777 /var/run/docker.sock
```

```bash
/usr/local/bin/minikube start --force --driver=docker
```

**<mark>STEP 5</mark>**

clone our project from git-hub

change directory

```bash
cd /opt
```

```bash
sudo git clone https://github.com/divyasatpute/docker-kubernates-migration.git
```

**<mark>STEP 6 -</mark>**

Install kubectl

```bash
sudo curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.20.4/2021-04-12/bin/linux/amd64/kubectl
```

```bash
sudo chmod +x ./kubectl
```

```bash
mkdir -p $HOME/bin
```

```bash
cp ./kubectl $HOME/bin/kubectl
```

```bash
export PATH=$HOME/bin:$PATH
```

```bash
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
```

```bash
source $HOME/.bashrc
```

```bash
kubectl version --short –client
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724674316834/0ae89c67-7dd4-4e3e-b957-1a688e077144.png align="center")

**<mark>STEP 7 -</mark>**

cd Kubernetes folder and create the namespace

```bash
cd docker-kubernates-migration/
```

```bash
cd kubernetes/
```

```bash
kubectl apply -f namespace.yaml
```

**<mark>STEP 8</mark>**

Verify the namespace

```bash
kubectl get ns
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724674422730/3804eac3-0cb9-48f2-afdf-b44f5e6be2f9.png align="center")

**<mark>STEP 9 -</mark>**

Create the configmap

```bash
kubectl apply -f configmap.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724674552363/0f915c84-1a20-43d2-a33e-46e6a22305ff.png align="center")

**<mark>STEP 10 -</mark>**

Create the Secrets

```bash
kubectl apply -f secret.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724674595402/248b159f-6938-446c-8605-0e5b7f5b57d5.png align="center")

**<mark>STEP 11</mark>**

Create the Persistent volume

```bash
kubectl apply -f persistent-volume.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724679753383/a0529c1c-0555-4c17-b7c0-25102c5227bf.png align="center")

**<mark>STEP 12</mark>**

Create the Persistent volume claim

```bash
kubectl apply -f persistent-volume-claim.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724679820274/7c2f7b02-1a3b-4139-ad8e-4922ff6a5483.png align="center")

**<mark>STEP 13 -</mark>**

Create the web deployment

```bash
kubectl apply -f web-deployment.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724679911655/83a42d64-331e-43be-8f88-00d38022c339.png align="center")

**<mark>STEP 14</mark>**

```bash
kubectl apply -f db-deployment.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724679985122/35a1550d-a3e7-4dba-93aa-9abb5d154d33.png align="center")

**<mark>STEP 15 -</mark>**

\- Create the service for web app DB

```bash
kubectl apply -f web-service.yaml
```

```bash
kubectl apply -f db-service.yaml
```

## **<mark>Test Result</mark>**

pod successfully up and running

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724680140733/56344376-5963-4ca5-96e7-f0c7a1f2d875.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724685659389/b90533d3-2c00-41f7-b1e6-5d447c17b6b8.png align="center")