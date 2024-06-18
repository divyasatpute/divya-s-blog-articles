---
title: "🎉 Building and Testing a Flask App with Docker: A Step-by-Step Guide 🚀"
seoTitle: "docker project simple"
datePublished: Tue Jun 18 2024 17:46:17 GMT+0000 (Coordinated Universal Time)
cuid: clxkp4ah8000209ld3obeg6pf
slug: building-and-testing-a-flask-app-with-docker-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718731264844/ad5b885c-41aa-49f5-bcf5-99f8d70beef9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1718732748614/fa993a9d-d479-4294-a004-e723440d3519.png
tags: docker, aws, devops, tws, diu

---

Creating and testing a Flask application using Docker can streamline your development process, ensuring consistency across different environments. This guide will walk you through the steps to set up and test a Flask application using Docker. Let's get started!

📝 Prerequisites

Before we begin, make sure you have the following installed:

* install Docker on your AWS machine
    
* AWS EC2 Machine
    

### 🛠 Step-by-Step Guide

1\. 📂 Set Up Your Project Directory

clone my repo on Github :

[https://github.com/divyasatpute/Docker-material/tree/master/FLASK](https://github.com/divyasatpute/Docker-material/tree/master/FLASK)

```bash
git clone https://github.com/divyasatpute/Docker-material.git
```

2. Change directory
    
    ```bash
    cd Docker
    ```
    
    Go to directory where is your Dockerfile
    

```bash
cd FLASK
```

🐳 Create a Dockerfile

```bash
# Use a specific version of Python with Alpine
FROM python:2.7-alpine3.10

# Set the working directory
WORKDIR /usr/src/app

# Install dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application files
COPY app.py ./
COPY templates/index.html ./templates/

# Expose the port the app runs on
EXPOSE 5000

# Define the command to run the application
CMD ["python", "app.py"]
```

🚀 Build Your Docker image

```bash
docker build -t divyasatpute/sanity-test .
```

Run your container

```bash
docker run -p 8080:5000 --name testcase divyasatpute/sanity-test
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718729375894/c63eae3b-9f58-4022-b2ea-2170b97f4e5b.jpeg align="center")

Now ✅ Testing Your Flask App

🌐 Access Your Flask Application

Copy public IP of your Instance and paste on tab

127.152.55.44:8080

## 🎉 Conclusion

By following these steps, you've successfully deployed your Flask application using Docker and exposed it to the internet with a public IP address. This setup is suitable for testing and development purposes. For production, consider additional steps for security, scalability, and performance optimization. Happy coding! 🚀

### Here are my POC Result

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718730049126/e541ec76-a0d2-4d86-9991-e1f3edfd3626.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718730060005/d2578261-b1f2-4139-8b2c-fee9e1923912.jpeg align="left")