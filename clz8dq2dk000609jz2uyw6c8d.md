---
title: "🌟 Ansible: The Magic Wand of IT Automation ✨"
seoTitle: "Ansible: Essential IT Automation Tool"
seoDescription: "Simplify IT automation with Ansible: a guide for installation, configuration, and playbooks for developers and sysadmins"
datePublished: Tue Jul 30 2024 12:13:28 GMT+0000 (Coordinated Universal Time)
cuid: clz8dq2dk000609jz2uyw6c8d
slug: ansible-the-magic-wand-of-it-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722319093229/ce3ce7c1-92df-40cb-82b4-b7d4842f1942.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722341507131/f853bf27-7334-4f2d-9c0d-b6087a3d82af.png
tags: ansible, devops, devops-articles, ansible-playbook, tws, diu

---

🚀🚀**What we learn in this Blog**🚀🚀

1. What is Ansible ??🤔✨
    
2. Configuration Management🤖
    
3. Push Based vs Pull Based📈
    
4. How to install Ansible
    
5. Host Inventory
    
6. YAML
    
7. Playbooks
    
8. Hands on
    
9. Conclusion.
    

---

**Unlocking the Power of Ansible: A Brief Guide** 🚀

***Hey there, tech adventurers! 🌟***

Ready to level up your IT game? Say hello to **Ansible**, the magical tool that makes managing your servers as easy as waving a wand. 🪄 Whether you’re a sysadmin, developer, or just a curious soul, Ansible is here to sprinkle some automation fairy dust over your infrastructure. Let’s dive into why Ansible is your new best friend! 🤖

### 🌐 What is Ansible?

Ansible is an open-source automation tool that simplifies IT orchestration, configuration management, and application deployment. It uses a simple, human-readable language (YAML) to define tasks, making automation accessible to everyone. 📜

Ansible is one among the DevOps Configuration management tools which is famous for its simplicity. It is an open source software developed by Michael DeHaan and its ownership is on RedHat.

Ansible is an open source IT configuration Management, Deployement & Orchestration tool.

This tool is very simple to use yet powerful enough to automate complex multi-tier IT application environments.

The main component of ansible are playbooks. configuration management and deployment.

just you want to specify what state you want the system to be in and ansible take care of it.

Ansible was written in python.

### 📊 Key Features of Ansible

* **Agentless**: No need to install agents on managed nodes, reducing complexity and overhead. 🖥️🔗
    
* **Versatile**: Works seamlessly across diverse platforms including Linux, Windows, and cloud environments. 🌍
    
* **Scalable**: From managing a few servers to thousands, Ansible scales effortlessly. 📈
    
* **Community-driven**: Continuously evolving with contributions from a vibrant community of users and developers. 🤝
    

### Configuration Management 🌟

**Configuration Management**: Automate server setups, software installations, and system configurations.

It is a method through which we automate admin task.

Configuration Management tool turns your code into Infrastructure.

so your code would be testable, repeatable and Versionable.

Infrastructure refers to the composite of -

* software
    
* Network
    
* People
    
* Process
    

### Push Based vs Pull Based

Tools like Puppet and chef are pull based

**Agent on the server periodically checks for the configuration information from central server (master)**

Ansible is Push Based

**Central server pushes the configuration information on target servers. You control when the changes are made on the servers**

<mark>(Ansible send notification to host servers to perform task )</mark>

### What Ansible can do ??

* Configuration Management
    
* App Deployment
    
* Continous Delivery
    

### 🧙‍♂️ **How Does Ansible Work?**

Ansible works by connecting to your nodes and pushing out a small program called Ansible Module to them .

Then Ansible executed these modules and removed them after finished. The library of module can reside on any machine. and there are no daemons ,servers, or databases required.

The Management node is the controlling node that controls the entire execution of the playbook.

The inventory file provide the list of hosts where the Ansible modules to be run.

The management node makes an SSH connection and executes the small modules on the host's machine and install the software.

Ansible removes the modules once those are installed so expertly.

It connect to the host machine executes the instructions, and if it is successfully installed, then remove that code in which one was copied on the host machine.

Ansible basically consists of three components

1. **Managed Nodes**🛠️
    
    Managed Nodes are stored in the hosts file for Ansible Automation.
    
2. **Ansible Playbooks**📚
    
    Ansible playbooks are expressed in YAML format and server as the repository for the various tasks that will be executed on the Managed Nodes (host)
    
    Playbooks are a collection of tasks that will be run on one or more hosts.
    

**Inventory File**🔧

Ansible's inventory hosts file is used to list and group your servers. its default location is /etc/ansible/hosts

> Note: In inventory host file we can mention IP address or Hostname also

**Sample of Inventory file**

```ini
[webservers]
web1.example.com
#web2.example.com

[databases]
192.168.1.20
192.168.1.21
db1.example.com
db2.example.com
```

**Important Points about Ansible Inventory File**

1. **Default Location**: The default location for the inventory file is `/etc/ansible/hosts`.
    
2. **Format**: The inventory file can be in INI or YAML format. The INI format is more common and straightforward.
    
3. **Grouping**: Hosts can be grouped into categories, such as `[webservers]` or `[databases]`, to apply tasks to multiple hosts simultaneously.
    
4. **Hostnames and IP Addresses**: You can list hosts by their hostnames or IP addresses.
    
5. **Variables**: You can define variables for groups or individual hosts within the inventory file. These variables can be used in playbooks to customize tasks.
    
6. **Dynamic Inventory**: Ansible supports dynamic inventory scripts, which can pull inventory data from external sources like cloud providers.
    
7. **Nested Groups**: Groups can be nested within other groups, allowing for more complex and hierarchical organization of hosts.
    
8. **Aliases**: Hosts can have aliases for easier reference in playbooks.
    
9. **Comments**: Lines starting with `#` are treated as comments and are ignored by Ansible.
    

### 📦Ansible setup 📦

Create Ubuntu system in AWS (free tier eligible) EC2 machine

1. Ansible system
    
2. Host system (it could 100 machine according to your requirement)
    

**<mark>This is optional step you can also skip but its is best practice to create ansible user</mark>**

Connect to the all the machine using Git-bash and create ansible user by following command .

```bash
sudo useradd ansible
sudo passwd ansible
```

Now confirm the password

Open the **visudo** and configure below detail

```bash
ansible All=(All) NOPASSWD:ALL
```

Now open vi/etc/ssh/sshd\_config file and <mark>comment</mark> the **PasswordAuthentication no**

and <mark>un-comment </mark> the **PasswordAuthentication yes**

```bash
sudo vi /etc/ssh/sshd_config
#PasswordAuthentication no
PasswordAuthentication yes
```

Restart the server

```bash
sudo service sshd restart
```

> Note : Do all above steps on every machine , this steps optional but it is highly recommended its is a best practice.

### <mark>Install Ansible in control node</mark>

***from here you don't miss any step***

Switch to Ansible User

```bash
sudo su ansible
```

Install packages

```bash
 sudo apt-add-repository ppa:ansible/ansible
```

update the packages

```bash
sudo apt update -y
```

Install ansible

```bash
sudo apt install ansible -y
```

Now check version

```bash
ansible --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722187189768/9670012d-ef1c-44a3-b2f8-1e05e84df78c.jpeg align="center")

create folder

```bash
mkdir keys
```

**Now copy the .pem file from your local to remote Machine by using scp command (run this command on your local )**

```bash
 scp -i "divya.pem" divya.pem ubuntu@ec2-13-127-5-106.ap-south-1.compute.amazonaws.com:/home/ubuntu/keys
```

> verify that your .pem file (key\_file) is present on keys folder which we cerate

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722187617890/540af7b5-a1ce-4970-847f-3500519a5361.png align="center")

Now go to your hosts file (Inventory file) and make some configuration like **<mark>Host_IP</mark>**

and pass variable **<mark>(all:vars) </mark>** where you can specify you **<mark>key file</mark>** location

> **Reverify that you configure all detail correctly**

```bash
sudo vim /etc/ansible/hosts
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722187950510/14c3cbd5-b9cb-4068-941a-33ad8d16f358.png align="center")

Give permission to your key

```bash
chmod 600 /home/ubuntu/keys/divya.pem
```

check your connectivity (**that your master node attach to host node or not**)

```bash
ansible all -m ping
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722189005247/60ad5e03-3ceb-4b9e-ad44-99d8fea336b3.jpeg align="center")

**Heyyyyyy hurayyyyy** with this Ansible setup is <mark>completed</mark>

### Ansible Ad Hoc Commands

Ansible ad hoc commands are a powerful feature that allows you to run simple commands or tasks directly on managed nodes without needing to write a full playbook. This can be useful for quick checks, debugging, or performing one-off tasks.

### **Basic Syntax for Ansible Ad Hoc Commands**

The general syntax for running an ad hoc command is:

```bash
ansible [Hostgroup,ip,hostname] -m [module] -a "[command]"
```

Where:

* `[group,ip,Hostname]` is the host or group of hosts on which you want to run the command.
    
* `-m [module]` specifies the Ansible module to use (e.g., `command`, `shell`, `ping`).
    
* `-a "[command]"` specifies the arguments for the module.
    

**Common Examples of Ansible Ad Hoc Commands**

1. **ansible all -m ping** = Use the `ping` module to check connectivity to the hosts
    
2. **ansible all -m shell -a "df -h"** =Use the `shell` module to execute a command. For example, to check the disk usage on all hosts
    
3. **ansible all -m shell -a "uptime"** =To check the uptime of all hosts
    
4. **ansible all -m copy -a "src=/path/to/file.txt dest=/tmp/file.txt"** =Use the `copy` module to copy a file from the control node to the managed nodes. For example, to copy `file.txt` to `/tmp` on all nodes
    
5. **ansible all -m apt -a "name=vim state=present** =Use the `apt` module (for Debian-based systems) to install a package
    
6. **ansible all -m service -a "name=nginx state=restarted**"=Use the `service` module to start, stop, or restart services. For example, to restart the `nginx` service on all hosts
    
7. **ansible all -m apt -a "name=vim state=absent" --become** =Use the `yum` or `dnf` module to remove software packages. For example, to uninstall `vim`
    
8. **ansible all -m command -a "systemctl status nginx"** =Check Status of a Service
    
9. **ansible all -m command -a "ip a"** =Get Network Interfaces
    
10. **ansible all -m file -a "path=/tmp/newdir state=directory" --become** =Create a Directory
    

> Irrespective of underlying OS which we can use to manage packages(software) using package manager in Ansible ????
> 
> Ans : Ansible introduced "package manager" to work with underlying package manager.

### 📜 YAML: The Friendly Data Serialization Format 🌟

### 🎯 What is YAML?

YAML stands for "YAML Ain't Markup Language" (a recursive acronym) or "Yet Another Markup Language." It's a human-readable data serialization standard that's often used for configuration files and data exchange. Think of YAML as the cool, more readable cousin of JSON and XML. 📜✨

### 🛠️ Practical Uses of YAML

Here are some common scenarios where YAML shines:

* **Configuration Files**: Applications like Docker and Kubernetes use YAML to define configurations and deployment setups. 🚢🛠️
    
* **Data Serialization**: YAML is great for storing and exchanging data between applications or systems. 🗃️
    
* **Documentation**: Many documentation tools use YAML to define metadata and configurations. 📚
    

### Ansible Playbooks

🌟 What is an Ansible Playbook?

An Ansible playbook is a YAML file that defines a set of tasks to be executed on remote systems. It’s a way to automate tasks like software installation, configuration changes, and system management. Think of it as a recipe for your infrastructure! 📜🍽️

### 📚 Key Components of a Playbook

1. **Play**: A play defines a set of tasks to be executed on a group of hosts. It’s like a chapter in your book of automation. 📖
    
2. **Tasks**: Tasks are the individual actions within a play. Each task uses an Ansible module to perform an action. 🛠️
    
3. **Modules**: Modules are the building blocks of tasks. They are predefined functions that Ansible uses to perform actions like installing packages, copying files, and more. 🔧
    
4. **Variables**: Variables store data that can be reused in playbooks. They make your playbooks flexible and dynamic. 🔢
    
5. **Handlers**: Handlers are special tasks that only run when notified by other tasks. They are great for managing services and performing actions only when changes occur. 🔄
    

### 🛠️ Writing Your First Ansible Playbook

Let’s get started with a simple example. We’ll create a playbook that installs Nginx webserver on a remote server and ensures the service is running.

### Step 1: Define the Playbook

Create a file named `setup-nginx.yml` and add the following content:

```bash
---
- name: Setup NGINX Server
  hosts: webservers
  become: yes
  tasks:
    - name: Install NGINX
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Start and enable NGINX service
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Deploy custom HTML page
      copy:
        src: index.html
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'
```

### Step 2: Create the HTML File

Create a file named `index.html` in the same directory as your playbook with the content you want to serve. For example: (**you can change html code according to your requirement)**

```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Learn with Divya - Magical & Fun</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
            color: #ffffff;
            background: linear-gradient(135deg, #ff7f50, #40e0d0, #d1a4a4);
            background-size: 300% 300%;
            animation: gradientAnimation 15s ease infinite;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
        }

        @keyframes gradientAnimation {
            0% { background-position: 0% 0%; }
            50% { background-position: 100% 100%; }
            100% { background-position: 0% 0%; }
        }

        .container {
            background: rgba(0, 0, 0, 0.7);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.5);
            max-width: 90%;
            width: 600px;
            margin: 20px;
            position: relative;
            overflow: hidden;
        }

        .container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('https://www.transparenttextures.com/patterns/white-sand.png');
            opacity: 0.2;
            z-index: 1;
        }

        .container h1 {
            margin-bottom: 20px;
            font-size: 2.8em;
            color: #ff1493;
            z-index: 2;
            position: relative;
        }

        .container p {
            margin-bottom: 20px;
            font-size: 1.2em;
            line-height: 1.6;
            color: #e0e0e0;
            z-index: 2;
            position: relative;
        }

        .container ul {
            list-style: none;
            padding: 0;
            margin: 0;
            font-size: 1.1em;
            color: #ffeb3b;
            z-index: 2;
            position: relative;
        }

        .container ul li {
            margin: 10px 0;
        }

        .button {
            display: inline-block;
            padding: 15px 25px;
            margin: 10px;
            font-size: 1.2em;
            color: #ffffff;
            background: #1e90ff;
            text-decoration: none;
            border-radius: 10px;
            transition: background 0.3s ease, transform 0.3s ease;
            z-index: 2;
            position: relative;
        }

        .button:hover {
            background: #ff6347;
            transform: scale(1.05);
        }

        .footer {
            margin-top: 30px;
            font-size: 0.9em;
            color: #cccccc;
            z-index: 2;
            position: relative;
        }

        @media (max-width: 768px) {
            .container {
                width: 90%;
                padding: 20px;
            }

            .container h1 {
                font-size: 2em;
            }

            .container p, .container ul li {
                font-size: 1em;
            }

            .button {
                padding: 12px 20px;
                font-size: 1em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Welcome to Learn with Divya! ✨</h1>
        <p>
            Dive into a world where knowledge meets magic. <strong>Learn with Divya</strong> brings you engaging content and enchanting tutorials.
        </p>
        <p>
            Discover:
            <ul>
                <li>🌟 Exciting Tutorials</li>
                <li>🧩 Interactive Tips</li>
                <li>🚀 Trendy Insights</li>
                <li>🎉 Fun Challenges</li>
            </ul>
        </p>
        <a href="https://learnwithdivya.hashnode.dev/" class="button">Explore the Blog</a>
        <div class="footer">
            &copy; 2024 Learn with Divya. All
```

### Explanation of the Playbook 📝

1. `name: Setup NGINX Server`: Describes the playbook.
    
2. `hosts: webservers`: Specifies the group of hosts where the tasks will be executed. You should have this group defined in your inventory file.
    
3. `become: yes`: Indicates that the tasks require elevated privileges (sudo).
    

#### Tasks:

```bash
- name: Install NGINX
  apt:
    name: nginx
    state: present
    update_cache: yes
```

* `name: nginx`: The package name for NGINX.
    
* `state: present`: Ensures the NGINX package is installed.
    
* `update_cache: yes`: Updates the package cache before installing.
    
    **2) Start and Enable NGINX Service**:
    
* ```bash
        - name: Start and enable NGINX service
          service:
            name: nginx
            state: started
            enabled: yes
    ```
    
    * `state: started`: Ensures the NGINX service is running.
        
    * `enabled: yes`: Configures the service to start on boot.
        
    
    **3) Deploy Custom HTML Page**:
    

```bash
  - name: Deploy custom HTML page
    copy:
      src: index.html
      dest: /var/www/html/index.html
      owner: www-data
      group: www-data
      mode: '0644'
```

* `src: index.html`: The source HTML file to copy.
    
* `dest: /var/www/html/index.html`: The destination path on the remote server.
    
* `owner: www-data`: Sets the file owner.
    
* `group: www-data`: Sets the file group.
    
* `mode: '0644'`: Sets the file permissions.
    

### Step 3: Run the Playbook

Execute the playbook using the `ansible-playbook` command:

```bash
ansible-playbook setup-nginx.yml
```

**before you access the application open all traffic rule in your Inbound rule**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722315827743/575794fb-ddec-41a2-a5c8-ac89f9e085c9.png align="center")

Access your application Now : **URL : http : // EC2-VM-Public-IP**

### <mark>Test Results :</mark>

**Connecting host node success**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722316065212/6bb4c19e-b5ca-4c36-808a-b928f23e0d62.png align="center")

**Ansible playbook works : Task completed**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722315683846/cd948240-5428-49d3-9e15-e2379c1ed493.png align="center")

**Access your application paste host node IP address on browser : website Deploy**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722315954508/c0c4c826-715d-456e-ad18-a3804da36fca.png align="center")

### Conclusion 🎉

With this playbook, you’ve automated the installation and configuration of NGINX and deployed a custom HTML page. Playbooks like this one save time and ensure consistency across your servers. 🚀

This command will apply the tasks defined in your playbook to the hosts specified. You’ll see output showing the progress of each task. 🛠️📈

**That’s a wrap on our magical journey through Ansible!** 🚀✨ From the basics to advanced features, Ansible is a powerful tool that can transform your IT operations. Dive in, explore, and let automation make your life easier and more fun! 🎉🌟

Feel free to leave your thoughts, questions, or Ansible tips in the comments below. Happy automating! 🤖💪

---