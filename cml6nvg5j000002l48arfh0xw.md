---
title: "What is Amazon EC2?"
seoTitle: "Understanding Amazon EC2"
seoDescription: "Discover Amazon EC2, a scalable cloud computing service that lowers hardware costs and enables fast application deployment in the AWS cloud"
datePublished: Tue Feb 03 2026 13:55:34 GMT+0000 (Coordinated Universal Time)
cuid: cml6nvg5j000002l48arfh0xw
slug: what-is-amazon-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1770126768279/89241e8d-01dd-4fd3-9d67-2e10c87b0e8a.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1770126863835/5c578e2f-f8a2-4965-9e2c-8110868ae099.png
tags: ec2, aws, aws-certified-solutions-architect-associate, aws-cdk, tws, teacode1122

---

Amazon Elastic Compute Cloud (Amazon EC2) provides on-demand, scalable computing capacity in the Amazon Web Services (AWS) Cloud. Using Amazon EC2 reduces hardware costs so you can develop and deploy applications faster. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage. You can add capacity (scale up) to handle compute-heavy tasks, such as monthly or yearly processes, or spikes in website traffic. When usage decreases, you can reduce capacity (scale down) again.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770115827019/39106880-61c7-4906-b575-54c87b185afd.png align="center")

## **Features of Amazon EC2**

  
Compute services

Amazon EC2 (Elastic Compute Cloud) for flexibility and scalable computing power, and AWS Lambda to run code on demand without managing servers, so you only pay for the compute time you use.

Amazon EC2 provides the following high-level features:

**Instances**

Virtual servers.

**Amazon Machine Images (AMIs)**

Preconfigured templates for your instances that package the components you need for your server (including the operating system and additional software).

**Instance types**

Various configurations of CPU, memory, storage, networking capacity, and graphics hardware for your instances.

**Amazon EBS volumes**

Persistent storage volumes for your data using Amazon Elastic Block Store (Amazon EBS).

**Instance store volumes**

Storage volumes for temporary data that is deleted when you stop, hibernate, or terminate your instance.

**Key pairs**

Secure login information for your instances. AWS stores the public key and you store the private key in a secure place.

**Security groups**

A virtual firewall that allows you to specify the protocols, ports, and source IP ranges that can reach your instances, and the destination IP ranges to which your instances can connect.

## **Pricing for Amazon EC2**

  
Amazon EC2 provides the following pricing options:

**Free Tier**

You can get started with Amazon EC2 for free. To explore the Free Tier options, see [AWS Free Tier](https://aws.amazon.com/free/).

**On-Demand Instances**

Pay for the instances that you use by the second, with a minimum of 60 seconds, with no long-term commitments or upfront payments.

**Savings Plans**

You can reduce your Amazon EC2 costs by making a commitment to a consistent amount of usage, in USD per hour, for a term of 1 or 3 years.

**Reserved Instances**

You can reduce your Amazon EC2 costs by making a commitment to a specific instance configuration, including instance type and Region, for a term of 1 or 3 years.

**Spot Instances**

Request unused EC2 instances, which can reduce your Amazon EC2 costs significantly.

**Dedicated Hosts**

Reduce costs by using a physical EC2 server that is fully dedicated for your use, either On-Demand or as part of a Savings Plan. You can use your existing server-bound software licenses and get help meeting compliance requirements.

**On-Demand Capacity Reservations**

Reserve compute capacity for your EC2 instances in a specific Availability Zone for any duration of time.

**Per-second billing**

Removes the cost of unused minutes and seconds from your bill.

For a complete list of charges and prices for Amazon EC2 and more information about the purchase models, see [Amazon EC2 pricing](https://aws.amazon.com/ec2/pricing/).

### **Estimates, billing, and cost optimization**

To create estimates for your AWS use cases, use the [AWS Pricing Calculator](https://calculator.aws/#/).

To estimate the cost of transforming **Microsoft workloads** to a modern architecture that uses open source and cloud-native services deployed on AWS, use the [AWS Modernization Calculator for Microsoft Workloads](https://modernization.calculator.aws/microsoft/workload).

To see your bill, go to the **Billing and Cost Management Dashboard** in the [AWS Billing and Cost Management console](https://console.aws.amazon.com/billing/). Your bill contains links to usage reports that provide details about your bill. To learn more about AWS account billing, see [AWS Billing and Cost Management User Guide](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/).

If you have questions concerning AWS billing, accounts, and events, [contact AWS Support](https://aws.amazon.com/contact-us/).

To calculate the cost of a sample provisioned environment, see [Cloud Economics Center](https://aws.amazon.com/economics/). When calculating the cost of a provisioned environment, remember to include incidental costs such as snapshot storage for EBS volumes.

You can optimize the cost, security, and performance of your AWS environment using [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/).

You can use AWS Cost Explorer to analyze the cost and usage of your EC2 instances. You can view data up to the last 13 months, and forecast how much you are likely to spend for the next 12 months. For more information, see [Analyzing your costs and usage with AWS Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html) in the *AWS Cost Management User Guide*.

## Step-by-Step: Create an EC2 Instance 🚀

Follow these **simple and clear steps** to create your first EC2 instance on AWS:

### Step 2: Open EC2 Service

* Search for **EC2** in the search bar
    
* Click on **EC2 → Instances → Launch Instance**
    

---

### Step 3: Choose an AMI (OS)

* Select an **Amazon Machine Image (AMI)**
    
* Recommended for beginners:
    
    * ✅ Amazon Linux 2 (Free Tier)
        
    * Ubuntu (optional)
        

---

### Step 4: Choose Instance Type

* Select instance size
    
* Choose **t2.micro** (Free Tier eligible)
    
* Click **Next** or **Continue**
    

---

### Step 5: Configure Key Pair

* Create a new key pair or select existing one
    
* Download the **.pem file**
    
* Keep it safe (used for SSH login)
    

---

### Step 6: Configure Security Group

* Create a new security group
    
* Allow required ports:
    
    * SSH – Port 22 (Your IP)
        
    * HTTP – Port 80 (Anywhere)
        
    * HTTPS – Port 443 (Optional)
        

---

### Step 7: Configure Storage

* Default storage is **8 GB EBS**
    
* You can increase size if needed
    
* Keep default for practice
    

---

### Step 8: Review & Launch

* Review all configurations
    
* Click **Launch Instance**
    

🎉 Your EC2 instance is created successfully!

---

### Step 9: Get Public IP Address

* Go to **EC2 → Instances**
    
* Select your instance
    
* Copy **Public IPv4 Address**
    

---

### Step 10: Connect to EC2 (Linux)

ssh -i key.pem ec2-user@public-ip

```plaintext
ssh -i key.pem ec2-user@public-ip
```

Now you are inside your EC2 server 🎯

## Connecting to EC2 Instance 🔗

Using SSH:

```plaintext
ssh -i key.pem ec2-user@public-ip
```

Once connected, you can:

* Install packages
    
* Run applications
    
* Configure services
    

## Final Thoughts 🎯

AWS is not just a cloud platform—it is a **career‑shaping skill**. Start small, practice daily, and build real projects.

If you master AWS fundamentals, the cloud world opens endless opportunities for you.

🚀 **Keep learning. Keep building. Welcome to the Cloud!**