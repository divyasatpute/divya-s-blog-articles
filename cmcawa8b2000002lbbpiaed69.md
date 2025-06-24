---
title: "🚀 DPDzero DevOps Intern Assignment: Nginx Reverse Proxy with Docker Compose"
datePublished: Tue Jun 24 2025 19:04:44 GMT+0000 (Coordinated Universal Time)
cuid: cmcawa8b2000002lbbpiaed69
slug: dpdzero-devops-intern-assignment-nginx-reverse-proxy-with-docker-compose
tags: assignment-help, tws, teacode

---

---

👩‍💻 **By Divya V. Satpute**

---

## 📌 Overview

As part of the DPDzero DevOps Internship Assignment, I was asked to containerize two services and expose them behind an Nginx reverse proxy using Docker Compose.

This blog will help you:

* Understand the technical setup
    
* Follow step-by-step CLI and Docker commands
    

---

## 🗂️ Project Folder Structure

```bash
.
├── docker-compose.yml
├── nginx/
│   └── nginx.conf
├── service_1/
│   ├── Dockerfile
│   └── main.go
├── service_2/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
```

---

## 🎬 Setup Steps

---

### 🎯 Step 1: Clone and Understand the Project

📖 Explanation

> "We start by cloning the project and looking at its structure. It has two services: one in Go and one in Python. Plus, there's an Nginx config file and a `docker-compose.yml`."

---

### 🛠️ Step 2: Dockerfile for Service 1 (Go)

📄 `service_1/Dockerfile`:

```Dockerfile
FROM golang:1.21-alpine

WORKDIR /app
COPY . .
RUN go build -o service1

CMD ["./service1"]
```

📖 Explanation**:**

> "In the Go service, we build the binary using `go build` and run it as the container starts. The service exposes `/hello` and `/ping` routes on port 8001."

---

### 🐍 Step 3: Dockerfile for Service 2 (Flask)

📄 `service_2/Dockerfile`:

```Dockerfile
FROM python:3.10-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

CMD ["python", "app.py"]
```

📖 Explanation**:**

> "For the Python Flask app, we install dependencies from `requirements.txt` and run `app.py`, which listens on port 8002. It also has `/hello` and `/ping` routes."

---

### 🧠 Step 4: Define Services in Docker Compose

📄 `docker-compose.yml`:

```yaml
version: '3.8'

services:
  service1:
    build: ./service_1
    container_name: service1-container
    expose:
      - "8001"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8001/hello"]
      interval: 10s
      timeout: 5s
      retries: 3

  service2:
    build: ./service_2
    container_name: service2-container
    expose:
      - "8002"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8002/hello"]
      interval: 10s
      timeout: 5s
      retries: 3

  nginx:
    build: ./nginx
    ports:
      - "8080:80"
    depends_on:
      service1:
        condition: service_healthy
      service2:
        condition: service_healthy
```

📖 Explanation**:**

> "Using Docker Compose, I defined all three services. I added health checks to wait for Go and Python apps to be ready before Nginx starts."

---

### 🌐 Step 5: Nginx as Reverse Proxy

📄 `nginx/nginx.conf`:

```nginx
events {}

http {
    access_log /var/log/nginx/access.log;

    server {
        listen 80;

        location /service1/ {
            proxy_pass http://service1:8001/;
        }

        location /service2/ {
            proxy_pass http://service2:8002/;
        }
    }
}
```

📖 Explanation**:**

> "The Nginx config listens on port 80. When you access `/service1/`, it sends traffic to the Go app, and `/service2/` routes to the Python app."

---

### 🧪 Step 6: Build and Run

🔧 **Command:**

```bash
docker-compose up --build -d
```

📖 Explanation**:**

> "I built and launched all services using `docker-compose up`. The `-d` flag means detached mode so it runs in the background."

---

### 🔍 Step 7: Testing Locally

🔧 Test individual services:

```bash
curl http://localhost:8001/hello
curl http://localhost:8002/hello
```

Test Nginx reverse proxy:

```bash
curl http://localhost:8080/service1/hello
curl http://localhost:8080/service2/hello
```

📖 Explanation**:**

> "I tested the services individually and via Nginx reverse proxy. Everything responded with JSON messages confirming that routing worked perfectly."

---

### 🌐 Step 8: EC2 Deployment (Optional)

If you're on AWS EC2:

🔧 Ensure you:

* Open **8080, 8001, 8002, 22** in the EC2 Security Group
    
* Run the same `docker-compose` commands
    
* Visit in browser:  
    `http://<public-ip>:8080/service1/hello`
    

📖 Explanation**:**

> "After opening ports in AWS security group, I accessed the services using my EC2 public IP with proper paths. It worked in the browser as expected."

---

## 🧪 Output Sample

```json
curl http://localhost:8080/service1/hello
{"message": "Hello from Service 1"}

curl http://localhost:8080/service2/hello
{"message": "Hello from Service 2"}
```

---

## 🎁 Bonus: Health Checks Work!

Try this:

```bash
docker inspect --format='{{json .State.Health}}' dpdzero-devops-intern-assignment-service1-1
```

📖 Explanation**:**

> "Docker Compose now waits for services to be 'healthy' before starting Nginx. It makes the setup more robust and production-ready."

---

## 📚 Key Learnings

✅ Reverse proxy with Nginx  
✅ Docker Compose service orchestration  
✅ Health checks and container debugging  
✅ EC2 deployment and port access  
✅ Application containerization and cleanup

---

## 📌 Conclusion

This assignment helped me learn how to:

* Dockerize applications
    
* Build multi-service architecture
    
* Set up and debug reverse proxy routing
    
* Deploy and test on real cloud environments
    

🧡 Huge thanks to **DPDzero** for this practical and exciting DevOps opportunity!

---

## 🔗 Let's Connect

* [LinkedIn – Divya Satput](https://www.linkedin.com/in/divya-satpute-68666a300/)e
    
* [Instagram – @teacode1122](https://instagram.com/teacode1122)
    

---