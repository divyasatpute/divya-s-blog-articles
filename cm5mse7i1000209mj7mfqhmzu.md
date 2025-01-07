---
title: "Deploying Super Mario on Kubernetes"
seoTitle: "Mario on Kubernetes: A Deployment Guide"
seoDescription: "Deploy Super Mario on Kubernetes using AWS EKS. Follow detailed steps to relive 90s gaming nostalgia with scalable and reliable deployment"
datePublished: Tue Jan 07 2025 18:11:09 GMT+0000 (Coordinated Universal Time)
cuid: cm5mse7i1000209mj7mfqhmzu
slug: deploying-super-mario-on-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736272953568/646d4816-031f-4447-8c9f-287bc9df0eab.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1736273413681/7973d585-8dee-4c38-a381-1c128110fe54.png
tags: devops, tws, teacode

---

Hey folks, remember the thrill of 90’s gaming? Let’s step back in time and relive those exciting moments! With the game deployed on Kubernetes, it’s time to dive into the nostalgic world of Mario. Grab your controllers, it’s game time!

Super Mario is a classic game loved by many. In this guide, we’ll explore how to deploy a Super Mario game on Amazon’s Elastic Kubernetes Service (EKS). Utilizing Kubernetes, we can orchestrate the game’s deployment on AWS EKS, allowing for scalability, reliability, and easy management.

<mark>𝗚𝗶𝘁𝗛𝘂𝗯 𝗥𝗲𝗽𝗼𝘀𝗶𝘁𝗼𝗿𝘆 </mark> : https://github.com/divyasatpute/day13-project13-lets-fun-gamewithmario.git[  
<mark>𝗷𝗼𝗶𝗻</mark>](https://lnkd.in/dXrecTvd%EF%BF%BC%F0%9D%97%B7%F0%9D%97%BC%F0%9D%97%B6%F0%9D%97%BB) [<mark>𝘄𝗵𝗮𝘁𝘀𝗮𝗽�</mark>](https://lnkd.in/dXrecTvd)<mark>� 𝗴𝗿𝗼𝘂𝗽 𝗧𝗲𝗮𝗰𝗼𝗱𝗲 𝟭𝟭𝟮𝟮</mark>

### Prerequisites:

1. An <mark>Ubuntu Instance</mark>
    
2. <mark>IAM role</mark>
    
3. <mark>Terraform</mark> should be installed on instance
    
4. <mark>AWS CLI</mark> and <mark>KUBECTL</mark> on Instance
    

### LET’S DEPLOY

### STEP 1: Launch Ubuntu instance

1. **Sign in to AWS Console:** Log in to your AWS Management Console.
    
2. **Navigate to EC2 Dashboard:** Go to the EC2 Dashboard by selecting “Services” in the top menu and then choosing “EC2” under the Compute section.
    
3. **Launch Instance:** Click on the “Launch Instance” button to start the instance creation process.
    
4. **Choose an Amazon Machine Image (AMI):** Select an appropriate AMI for your instance. For example, you can choose Ubuntu image.
    
5. **Choose an Instance Type:** In the “Choose Instance Type” step, select `t2.micro` as your instance type. Proceed by clicking “Next: Configure Instance Details.”
    
6. **Configure Instance Details:**
    
    * For “Number of Instances,” set it to 1 (unless you need multiple instances).
        
    * Configure additional settings like network, subnets, IAM role, etc., if necessary.
        
    * For “Storage,” click “Add New Volume” and set the size to 8GB (or modify the existing storage to 8GB).
        
    * Click “Next: Add Tags” when you’re done.
        
7. **Add Tags (Optional):** Add any desired tags to your instance. This step is optional, but it helps in organizing instances.
    
8. **Configure Security Group:**
    
    * Choose an existing security group or create a new one.
        
    * Ensure the security group has the necessary inbound/outbound rules to allow access as required.
        
9. **Review and Launch:** Review the configuration details. Ensure everything is set as desired.
    
10. **Select Key Pair:**
    
    * Select “Choose an existing key pair” and choose the key pair from the dropdown.
        
    * Acknowledge that you have access to the selected private key file.
        
    * Click “Launch Instances” to create the instance.
        
11. **Access the EC2 Instance:** Once the instance is launched, you can access it using the key pair and the instance’s public IP or DNS.
    

Ensure you have necessary permissions and follow best practices while configuring security groups and key pairs to maintain security for your EC2 instance.

### STEP 2: Create IAM role

Search for IAM in the search bar of AWS and click on roles.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701788356974/d4f64b19-c42e-46ca-b2a5-470976c4403e.png?auto=compress,format&format=webp align="left")

Click on Create Role

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701788553074/3f9d2609-dab2-451a-9283-992305c84124.png?auto=compress,format&format=webp align="left")

Select entity type as AWS service

Use case as EC2 and click on Next.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701788684513/436954d5-ce61-420b-b882-5a37b3dc6b40.png?auto=compress,format&format=webp align="left")

For permission policy select Administrator Access (Just for learning purpose), click Next.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701788880922/d5ad58eb-aa16-4755-a163-42d54ec5c4a9.png?auto=compress,format&format=webp align="left")

Provide a Name for Role and click on Create role.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701789046126/d0610edd-f1fd-4c47-9fbe-e52be618dcda.png?auto=compress,format&format=webp align="left")

Role is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701789159661/ecdaba8f-64f9-4745-ba83-9eed724e07b9.png?auto=compress,format&format=webp align="left")

Now Attach this role to Ec2 instance that we created earlier, so we can provision cluster from that instance.

Go to EC2 Dashboard and select the instance.

Click on Actions –&gt; Security –&gt; Modify IAM role.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701789375582/9d936532-6404-4587-9f3e-b25be39095c8.png?auto=compress,format&format=webp align="left")

Select the Role that created earlier and click on Update IAM role.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701789544258/b3c244ff-b138-43b1-90d2-3faca8a7d07a.png?auto=compress,format&format=webp align="left")

Connect the instance to Mobaxtreme or Putty

### STEP 3: Cluster provision

Now clone this Repo.

```bash
https://github.com/divyasatpute/day13-project13-lets-fun-gamewithmario.git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736272636403/55e8f980-b1a9-46e6-bcee-a513d5bb14a6.png align="center")

change directory

```bash
cd day13-project13-lets-fun-gamewithmario/
```

Provide the executable permission to [script.sh](http://script.sh/) file, and run it.

```bash
sudo chmod +x script.sh
./script.sh
```

This script will install `Terraform, AWS cli, Kubectl, Docker.`

Check versions

```bash
docker --version
aws --version
kubectl version --client
terraform --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701790320134/14d34ce4-f8da-4906-8d0a-dae095c10cbf.png?auto=compress,format&format=webp align="left")

Now change directory into the EKS-TF

Run Terraform init

`NOTE: Don’t forgot to change the s3 bucket name in the backend.tf file`

```bash
cd EKS-TF
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701790560576/a49a9e80-a768-4b45-85f2-979e6fdc4c0f.png?auto=compress,format&format=webp align="left")

Now run terraform validate and terraform plan

```bash
terraform validate
terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701790675486/a1a62740-8969-468f-9674-9a2b05ff4d59.png?auto=compress,format&format=webp align="left")

Now Run terraform apply to provision cluster.

```bash
terraform apply --auto-approve
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701790814354/c0dce9bb-6c67-4a9d-904e-e9db168abf7a.png?auto=compress,format&format=webp align="left")

Completed in 10mins

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701790860982/b6ebdcbc-e5b7-4357-8041-a47e501b73d0.png?auto=compress,format&format=webp align="left")

Update the Kubernetes configuration

Make sure change your desired region

```bash
aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701790944797/2ab48d79-5a12-45f2-b8e8-a76bde77395c.png?auto=compress,format&format=webp align="left")

Now change directory back to day13-project13-lets-fun-gamewithmario/

```bash
cd ..
```

Let’s apply the deployment and service

**Deployment**

```bash
kubectl apply -f deployment.yaml
#to check the deployment 
kubectl get all
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701791307444/53f6b1ea-60fc-42ff-9681-7bbd9e0617dc.png?auto=compress,format&format=webp align="left")

Now let’s apply the service

**Service**

```bash
kubectl apply -f service.yaml
kubectl get all
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701791413429/4ab0cac5-dcc8-41e8-84db-e836b310cb14.png?auto=compress,format&format=webp align="left")

Now let’s describe the service and copy the LoadBalancer Ingress

```bash
kubectl describe service mario-service
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701791679951/7ec163e6-d960-4756-91b3-c5cbcdd62664.png?auto=compress,format&format=webp align="left")

Paste the ingress link in a browser and you will see the Mario game.

Let’s Go back to 1985 and play the game like children.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701791775730/7f8264f8-8690-4f13-be2d-ec037ca2384e.png?auto=compress,format&format=webp align="left")

This is official image by `MR CLOUD BOOK`

You can check in Docker-hub as well `sevenajay/mario:latest`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701792035335/99c0ab46-106a-4d39-a400-9d2768e4cc03.png?auto=compress,format&format=webp align="left")

### Destruction :

Let’s remove the service and deployment first

```bash
kubectl get all
kubectl delete service mario-service
kubectl delete deployment mario-deployment
```

Let’s Destroy the cluster

```bash
terraform destroy --auto-approve
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701792259898/67e29ff0-f72f-4da6-bad9-06445e1dd80e.png?auto=compress,format&format=webp align="left")

After 10mins Resources that are provisioned will be removed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701792351330/40fff85d-fe0c-4baf-a98d-ddac932ce71f.png?auto=compress,format&format=webp align="left")

Thank you for joining this nostalgic journey to the 90s! We hope you enjoyed rekindling your love for gaming with the deployment of the iconic Mario game on Kubernetes. Embracing the past while exploring new technologies is a true testament to the timeless allure of classic games. Until next time, keep gaming and reliving those fantastic memories! 👾🎮.