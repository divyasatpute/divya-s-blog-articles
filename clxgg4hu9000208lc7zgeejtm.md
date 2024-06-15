---
title: "🚀 Deploying a Simple Flask App with Docker"

---

Creating a Dockerized Flask app is a great way to ensure your application runs consistently across different environments. In this guide, we'll walk you through the process step-by-step using emojis for a fun twist! 😊

## 📝 Prerequisites

Before we start, make sure you have the following installed:

* 🐍 Python
    
* 🐳 Docker
    
* 💻 A code editor (like VS Code)
    
* 💻 EC2 Machine (AWS)
    

## 📂 Project Structure

### 🛠️ Step-by-Step Guide

1\. Set up EC2 machine and log-in using Gitbash and Install docker on EC2 machine

### 2.📦 Setting Up Your Flask App

```python
from flask import Flask
helloworld = Flask(__name__)
@helloworld.route("/")
def run():
    return "{\"message\":\"Hey there python\"}"

if __name__=="__main__":
    helloworld.run(host="0.0.0.0", port=int("3000"), debug=True)
```

### 3\. 📜 Listing Dependencies

Next, list your dependencies in `requirements.txt`.

**requirements.txt:**

```python
flask
```

### 4\. 🐳 Creating the Dockerfile

Now, create a `Dockerfile` to define your Docker image.

**Dockerfile :**

```python
FROM python:3-alpine3.15
WORKDIR /app
COPY . /app
RUN pip install -r requirement.txt
EXPOSE 3000
CMD python ./index.py
```

### 5\. 🏗️ Building the Docker Image

With your `Dockerfile` in place, build your Docker image.

```python
docker build -t divyasatpute/hey-python-flask:latest .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718451775631/8c285328-7ac9-4fbc-9c9a-e8fa1f6d9324.jpeg align="center")

### 6.🚢 Running the Docker Container

Once the image is built, run it using Docker.

```python
docker container run -d -p 3000:3000 divyasatpute/hey-python-flask:latest
```

### 🔍 Verify the Deployment

Open your web browser and navigate to [`http://localhost:`](http://localhost:5000)`3000`. You should see "Hey there python!" 🎉

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718451836062/48ff0aad-5d51-441c-a3ef-4caffd7b5a86.jpeg align="center")

Now Everything is working fine then our last step is only pending which is nothing but **PUSH** ON OUR **DOCKERHUB**

## 7 .Push Image in our ***DockerHub Account***

```python
docker push divyasatpute/hey-python-flask:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718451807513/664c38df-a9a8-44e5-aaaf-2abd32cd609d.jpeg align="center")

> Make sure that you can replace your own username and the things whenever its needed :

## 📋 Summary

* ✍️ Created a simple Flask app
    
* 📜 Listed dependencies in `requirements.txt`
    
* 🐳 Defined a Dockerfile
    
* 🏗️ Build the Docker image
    
* 🚢 Run the Docker container
    

---

**Congratulations! You've successfully Dockerized your Flask app! 🥳 Now your app can run consistently in any environment.**

### Here I am showing all the results you can also Refer :

Feel Free to ask or comment if you are facing some issue

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718451580842/d45de7e7-555d-41a2-a545-c4849bae0b0d.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718451701358/384a85dc-1ddb-41ab-9a23-1009fd7d1954.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718451719626/649272ed-106c-4eea-9ab4-769bb8f4e1e5.jpeg align="center")
