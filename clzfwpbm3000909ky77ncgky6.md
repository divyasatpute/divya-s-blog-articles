---
title: "Learn Ansible Automation: A Beginner to Expert Guide"
seoTitle: "Ansible Automation Guide for Beginners and Experts"
seoDescription: "Master Ansible with this guide, covering basics, advanced techniques, Vault, inventories, Galaxy, roles, and Tower"
datePublished: Sun Aug 04 2024 18:39:09 GMT+0000 (Coordinated Universal Time)
cuid: clzfwpbm3000909ky77ncgky6
slug: learn-ansible-automation-a-beginner-to-expert-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722787860404/28697054-47ef-435f-8ec1-c4de7cfc6392.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722796708355/9105faf5-b1c9-474d-a2b5-9fd1e271e3bc.png
tags: ansible, devops, ansible-playbook, tws, diu

---

Hello, automation enthusiasts! 🎉 Ready to embark on a thrilling journey through the world of Ansible? Whether you’re just starting or looking to supercharge your skills, this guide will walk you through everything from the basics to advanced techniques. Grab your gear, and let’s dive into the magical world of automation! 🧙‍♂️🛠️

### 1\. Getting Started: Your First Steps with Ansible 🏁🔧

* **What’s Ansible?** 🤔: Ansible is a powerful automation tool that uses simple YAML files to define and execute tasks across your infrastructure. It’s like having a personal assistant who follows your exact instructions to set up servers, deploy applications, and more!
    
* ### 📦Ansible setup 📦
    
    Install packages
    

```bash
sudo apt-add-repository ppa:ansible/ansible
sudo apt update -y
sudo apt install ansible -y
ansible --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722187189768/9670012d-ef1c-44a3-b2f8-1e05e84df78c.jpeg align="center")

* **<mark>Configuration Management 🌟</mark>**
    
    **Configuration Management**: Automate server setups, software installations, and system configurations.
    
* **<mark>Push Based vs Pull Based</mark>**
    
    Tools like Puppet and chef are pull based
    
    **Agent on the server periodically checks for the configuration information from central server (master)**
    
    Ansible is Push Based
    
    **Central server pushes the configuration information on target servers. You control when the changes are made on the servers**
    

<mark>(Ansible send notification to host servers to perform task )</mark>

* **<mark>Inventory File</mark>**<mark>🔧</mark>
    

Ansible's inventory hosts file is used to list and group your servers. its default location is /etc/ansible/hosts

> Note: In inventory host file we can mention IP address or Hostname also
> 
> **Inventory** 📋: This is your list of servers. It’s where you define which servers Ansible should manage. For example:

```bash
[webservers]
server1.example.com
server2.example.com
```

### **<mark>Ansible Playbooks</mark>**

**🌟 What is an Ansible Playbook?**

An Ansible playbook is a YAML file that defines a set of tasks to be executed on remote systems. It’s a way to automate tasks like software installation, configuration changes, and system management. Think of it as a recipe for your infrastructure! 📜🍽️

* **Playbooks** 📜: Think of playbooks as detailed recipes. They outline the steps needed to achieve your goals. Here’s a basic example:
    

```bash
- name: Install and start Apache
  hosts: webservers
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
    - name: Start Apache
      service:
        name: apache2
        state: started
```

> This playbook tells Ansible to install Apache on your web servers and then start the service.

### 2\. Adding Spice: Intermediate Techniques 🌶️🚀

**Now that you’ve got the basics, let’s add some flavor:**

### <mark>Vault in Ansible 🔐</mark>

### 📚 What is Ansible Vault?

Ansible Vault is a feature of Ansible that allows you to keep sensitive data such as passwords or keys in encrypted files, rather than as plaintext in your playbooks or roles. This ensures that sensitive information is protected even if your playbook is shared or stored in a public repository.

**<mark>🔑 Key Features</mark>**

* **Encryption and Decryption**: Securely encrypt and decrypt files.
    
* **Ease of Use**: Simple commands to integrate encryption into your workflow.
    

**Granular Control**: Encrypt entire files or specific variables.

### 🛠️ How to Use Ansible Vault

**<mark>1. Creating Encrypted Files</mark>**

To create a new encrypted file, use the `ansible-vault create` command:

```bash
ansible-vault create secrets.yml
```

This command will open your default text editor, allowing you to enter the sensitive data. Once you save and exit the editor, the file will be encrypted.

**<mark>2. Encrypting Existing Files</mark>**

You can encrypt an existing file using the `ansible-vault encrypt` command:

```bash
ansible-vault encrypt existing-file.yml
```

<mark>3. </mark> **<mark>Editing Encrypted Files</mark>**

To edit an encrypted file, use the `ansible-vault edit` command:

```bash
ansible-vault edit secrets.yml
```

This command will decrypt the file, open it in your default text editor, and then re-encrypt it once you save and exit.

**<mark>4. Decrypting Files</mark>**

If you need to decrypt a file, use the `ansible-vault decrypt` command:

```bash
ansible-vault decrypt secrets.yml
```

**<mark>5. Viewing Encrypted Files</mark>**

To view the contents of an encrypted file without editing it, use the `ansible-vault view` command:

```bash
ansible-vault view secrets.yml
```

## <mark>🌟 Understanding Handlers in Ansible 🌟</mark>

### 📚 What are Handlers?

Handlers are special tasks in Ansible that are triggered only when notified by other tasks. They are typically used to perform actions that should only occur if there has been a change in the system state. Common use cases include restarting a service after a configuration file has been updated or reloading a web server when its configuration changes.

### 🔑 Key Characteristics of Handlers

* **Conditional Execution**: Handlers are only run when notified by another task.
    
* **Idempotency**: They ensure actions are only performed when necessary.
    
* **Organization**: They help keep playbooks clean and manageable.
    
* **🛠️ How Handlers Work**
    
    ### **1\. Define a Handler**
    
    Handlers are defined in the same way as regular tasks but are placed under the `handlers` section.
    
* ```bash
      handlers:
        - name: restart apache
          service:
            name: httpd
            state: restarted
    ```
    
    ### 2\. **Notify a Handler**
    
    To notify a handler, use the `notify` directive in the task that may require the handler to run.
    

```bash
tasks:
  - name: copy apache configuration file
    copy:
      src: /path/to/httpd.conf
      dest: /etc/httpd/conf/httpd.conf
    notify:
      - restart apache
```

### **3\. Handler Execution**

Handlers are executed at the end of the playbook run, ensuring that the tasks have made all necessary changes before the handler is triggered.

---

## 🌌 Exploring Ansible Galaxy 🌌

### 📚 What is Ansible Galaxy?

Ansible Galaxy is a free service provided by Ansible that allows users to share and download roles. Roles in Ansible are a way of bundling automation content and can include tasks, handlers, variables, templates, and more. Galaxy helps you avoid reinventing the wheel by leveraging the work of the community.

### 🌟 Key Features

* **Discoverability**: Easily find and use roles created by the community.
    
* **Reusability**: Share your roles with others and reuse roles created by others.
    
* **Community Contributions**: Benefit from the expertise and contributions of a large community.
    

### 🔍 Finding Roles on Ansible Galaxy

You can browse roles on the Ansible Galaxy website or use the `ansible-galaxy` command-line tool to search for roles.

**🔗 Using the Ansible Galaxy Website**

Visit Ansible Galaxy to browse roles by category, popularity, or name. You can also see detailed information about each role, including documentation, dependencies, and ratings.

**🔧 Using the**`ansible-galaxy`**Command**

To search for roles from the command line, use the `ansible-galaxy search` command:

```bash
ansible-galaxy search <role_name>
```

For example, to search for Nginx roles:

```bash
ansible-galaxy search nginx
```

## 📦 Installing Roles

Once you've found a role you want to use, you can install it using the `ansible-galaxy install` command.

### 📝 Example Installation

To install a role named `geerlingguy.nginx`:

```bash
ansible-galaxy install geerlingguy.nginx
```

The role will be downloaded and stored in your default roles path (`/etc/ansible/roles` or `roles/` in your project directory).

## 🔧 Using Roles in Playbooks

After installing a role, you can include it in your playbooks. Here's an example of how to use the `geerlingguy.nginx` role in a playbook:

```bash
---
- hosts: webservers
  roles:
    - geerlingguy.nginx
```

### <mark>🛠️ Creating and Sharing Roles</mark>

### **<mark>Ansible Roles</mark>** <mark> 🛠️</mark>

Roles are abstraction on top of tasks and playbooks that let you structure your Ansible configuration in a modular and reusable format.

As you add more and more functionality and flexibility to your playbooks, they can become unwieldy and difficult to maintain.

Roles allow you to break down a complex playbook into separate , smaller chunks that can be coordinated by a central entry point.

**Key Components of a Role:**

* **Tasks** 📝: The actions that the role performs.
    
* **Handlers** 🚦: Special tasks that are triggered by other tasks (e.g., restarting a service after configuration changes).
    
* **Variables** 🔑: Settings that customize the role’s behavior.
    
* **Templates** 🖌️: Jinja2 templates used to create dynamic configuration files.
    
* **Files** 📁: Static files that the role needs (e.g., configuration files).
    
* **Defaults** ⚙️: Default values for variables that can be overridden.
    

**<mark>Creating a Role: Your First Step to Organization 🚀🏗️</mark>**

Let’s walk through creating a role from scratch. Imagine we’re building a role to set up a web server. Here’s how you can do it:

1. **Create the Role Directory** 📂:
    

```bash
ansible-galaxy init webserver
```

This command creates a directory named `webserver` with a predefined structure:

```bash
webserver/
├── defaults/
│   └── main.yml
├── files/
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
└── vars/
    └── main.yml
```

2. **Define Tasks** 🛠️:
    
    In `webserver/tasks/main.yml`, write the tasks to install and configure your web server:
    
    ```bash
    - name: Install Apache
      apt:
        name: apache2
        state: present
    
    - name: Start Apache
      service:
        name: apache2
        state: started
    ```
    
    3. **Add Handlers** 🚦:
        
    
    In `webserver/handlers/main.yml`, define any handlers that should be triggered:
    
    ```bash
    - name: Restart Apache
      service:
        name: apache2
        state: restarted
    ```
    
    4. **Set Default Variables** 🔑:
        
        In `webserver/defaults/main.yml`, set default values for variables:
        
        ```bash
        apache_port: 80
        ```
        
        5. Create Templates 🖌️: Place your Jinja2 templates in `webserver/templates/`. For instance, `apache.conf.j2` might look like this:
            
            ```bash
            <VirtualHost *:{{ apache_port }}>
                DocumentRoot /var/www/html
            </VirtualHost>
            ```
            
    
    6. **Define Role Metadata** 📋:
        

In `webserver/meta/main.yml`, provide metadata about the role:

```bash
galaxy_info:
  author: Your Name
  description: Role for setting up Apache web server
  company: Your Company
```

7. **<mark>Using Roles in Playbooks: Putting It All Together 🧩📜</mark>**
    

Once you have your role ready, using it in a playbook is straightforward. Here’s how you can apply the `webserver` role:

```bash
- name: Set up web servers
  hosts: webservers
  roles:
    - webserver
```

This playbook applies the `webserver` role to all hosts in the `webservers` group. Ansible will automatically look in the `webserver` role directory for the tasks, handlers, variables, and templates.

<mark>Congratulations! You’ve unlocked the secrets of Ansible roles and are ready to organize and reuse your automation tasks like a pro.</mark>

### 3\. Advanced Techniques: Unlocking the Power! 🔓💪

**Advanced Techniques: Unlocking the Power! 🔓💪**

### 🌍 Managing Ansible Inventories for Different Environments 🌍

In any robust infrastructure, managing different environments (such as development, testing, staging, and production) is essential. Ansible provides flexible inventory management, allowing you to define and use different inventories for various environments. This post will guide you through setting up and managing Ansible inventories for different environments efficiently.

### 🗂️ What is an Ansible Inventory?

An Ansible inventory is a collection of hosts (or nodes) that Ansible manages. It can be a simple static file, a dynamic script, or a combination of both. By organizing your inventory, you can target specific groups of hosts for different environments and streamline your automation processes.

### 📋 Static Inventory

Static inventories are the simplest way to define your hosts and groups. You can create separate inventory files for each environment.

### 📝 Example Inventory Files

#### Development Inventory (`inventories/dev`)

```bash
[webservers]
dev-web1 ansible_host=192.168.1.10

[dbservers]
dev-db1 ansible_host=192.168.1.11
```

#### Staging Inventory (`inventories/staging`)

```bash
[webservers]
staging-web1 ansible_host=192.168.2.10

[dbservers]
staging-db1 ansible_host=192.168.2.11
```

#### Production Inventory (`inventories/prod`)

```bash
[webservers]
prod-web1 ansible_host=192.168.3.10

[dbservers]
prod-db1 ansible_host=192.168.3.11
```

### 📦 Using Static Inventory Files

You can specify the inventory file when running Ansible commands:

```bash
ansible-playbook -i inventories/dev playbook.yml
ansible-playbook -i inventories/staging playbook.yml
ansible-playbook -i inventories/prod playbook.yml
```

## 🌐 Dynamic Inventory

Dynamic inventories allow you to generate inventory data dynamically from external sources such as cloud providers, databases, or custom scripts.

### 🗄️ Example: AWS EC2 Dynamic Inventory

1. **Install the**`boto3` library:
    
    ```bash
    pip install boto3
    ```
    
2. **Create a dynamic inventory script (**`aws_`[`ec2.py`](http://ec2.py)):
    
    ```python
    #!/usr/bin/env python
    
    import boto3
    import json
    
    def get_instances():
        ec2 = boto3.client('ec2')
        instances = ec2.describe_instances()
    
        inventory = {'_meta': {'hostvars': {}}}
        for reservation in instances['Reservations']:
            for instance in reservation['Instances']:
                if instance['State']['Name'] == 'running':
                    instance_id = instance['InstanceId']
                    inventory['_meta']['hostvars'][instance_id] = instance
    
        return inventory
    
    if __name__ == '__main__':
        print(json.dumps(get_instances()))
    ```
    
3. **Use the dynamic inventory script:**
    
    ```bash
    ansible-playbook -i aws_ec2.py playbook.yml
    ```
    

## 🧩 Combining Static and Dynamic Inventories

You can combine static and dynamic inventories to leverage the advantages of both. This is especially useful in complex environments where some hosts are static and others are dynamically provisioned.

### 📝 Example Inventory Directory Structure

```bash
plaintextCopy codeinventories/
├── dev
│   ├── hosts
│   └── aws_ec2.py
├── staging
│   ├── hosts
│   └── aws_ec2.py
├── prod
│   ├── hosts
│   └── aws_ec2.py
```

### 🗂️ `hosts` File

```bash
[webservers]
localhost ansible_connection=local
```

### 📦 Using Combined Inventory

Specify the inventory directory to use both static and dynamic sources:

```bash
ansible-playbook -i inventories/dev playbook.yml
ansible-playbook -i inventories/staging playbook.yml
ansible-playbook -i inventories/prod playbook.yml
```

## 🔄 Inventory Plugins

Ansible also supports inventory plugins that can fetch inventory data from various sources like cloud providers, containers, and more.

### 🛠️ Using the AWS EC2 Inventory Plugin

1. **Install the AWS EC2 inventory plugin:**
    
    ```bash
    pip install boto3 botocore
    ```
    
2. **Configure the plugin (**`inventories/dev/aws_ec2.yml`):
    
    ```bash
    plugin: aws_ec2
    regions:
      - us-east-1
    filters:
      instance-state-name: running
    keyed_groups:
      - key: tags.Name
        prefix: tag_Name_
    ```
    
3. **Use the inventory plugin:**
    
    ```bash
    ansible-inventory -i inventories/dev/aws_ec2.yml --list
    ansible-playbook -i inventories/dev/aws_ec2.yml playbook.yml
    ```
    

## 🌟 Best Practices for Managing Inventories

🧩 **Use Separate Inventory Files for Different Environments**

Maintain separate inventory files or directories for different environments to keep configurations organized and avoid accidental modifications.

### 🔒 Secure Sensitive Data

Use Ansible Vault to encrypt sensitive information in your inventory files, such as passwords or API keys.

```bash
ansible-vault encrypt inventories/prod/hosts
```

### 🚀 Automate Inventory Management

Use CI/CD pipelines and tools like Ansible Tower or AWX to automate inventory updates and manage secrets securely.

## Automation with Ansible Tower 🏰

### What is Ansible Tower? 🏰

Ansible Tower is a robust framework built on top of Ansible that provides a user-friendly web interface, role-based access control, job scheduling, and integrated notifications. It transforms your Ansible playbooks into a centralized automation tool that's easy to manage and scale.

### Key Features:

* **Web-based UI**: Manage your Ansible playbooks, inventory, and jobs through an intuitive interface.
    
* **Real-time Job Status**: Monitor the progress of your automation tasks in real-time.
    
* **Role-Based Access Control**: Secure your environment by controlling who can run and manage jobs.
    
* **Job Scheduling**: Automate tasks to run at specific times or intervals.
    
* **Integrated Notifications**: Get alerts on job status via email, Slack, or other channels.
    
* **REST API**: Integrate Ansible Tower with other tools and systems.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722795504021/52a278d1-9dc5-45e1-93d3-fd64cf4edbc6.png align="center")
    

## Conclusion 🎉

Ansible Tower is a game-changer for IT automation, providing a centralized, user-friendly platform for managing Ansible playbooks, inventories, and jobs. Its powerful features, such as real-time monitoring, job scheduling, and role-based access control, make it an essential tool for any organization looking to scale and secure their automation efforts. Whether you're new to automation or looking to enhance your existing workflows, Ansible Tower has the capabilities to take your IT operations to the next level.

Happy automating! 🤖✨

Thank you so much for referring my blog ! 🌟 really appreciate your support! If you found them helpful, feel free to like, share, or leave a comment! Your feedback means a lot to me and helps me create even better content. 😊 Thanks again! 🙌