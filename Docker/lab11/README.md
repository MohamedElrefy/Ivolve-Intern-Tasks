## 📘 Objective
This lab demonstrates how to manage **environment variables** in Docker at different stages — during **build** and **runtime** — using a simple **Flask** Python application.

---

## 🧰 Prerequisites
- Docker installed on your system  
- Git installed  
- Internet connection to clone the repository  

---

## 🚀 Steps

### 1️⃣ Clone the Repository
Clone the application code from GitHub:
```bash
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3
```
## 2️⃣ Create a Dockerfile

Write a Dockerfile with the following requirements:

Base image: python

Install Flask

Expose port 8080

Set default environment variables (APP_MODE, APP_REGION) for production

Run the app using python app.py

## 3️⃣ Build the Docker Image
```bash
docker build -t app-env .
```
## 4️⃣ Run the Container with Environment Variables in Different Ways
### 🧩 Case 1: Pass Environment Variables Directly in the Command

Run the container and set environment variables from the command line:
```bash
docker run -d -p 8080:8080 \
  -e APP_MODE=development \
  -e APP_REGION=us-east \
  --name app-env-dev app-env
```
### 🧾 Case 2: Pass Environment Variables from a File

Create a file named .env with the following content:
```bash
APP_MODE=staging
APP_REGION=us-west
```

Run the container using the environment file:
```bash
docker run -d -p 8080:8080 \
  --env-file .env \
  --name app-env-staging app-env
```
### 🏭 Case 3: Use Environment Variables from the Dockerfile

In the Dockerfile, environment variables are already defined as:
```bash
ENV APP_MODE=production
ENV APP_REGION=canada-west
```

So when you run the container without specifying anything:
```bash
docker run -d -p 8080:8080 --name app-env-prod app-env
```

It will use the production values from the Dockerfile.

## 5️⃣ Verify the Application

To test if your app is running correctly:
```bash
curl http://localhost:8080
```
## 6️⃣ Stop and Remove Containers
```bash
docker stop app-env-dev app-env-staging app-env-prod
docker rm app-env-dev app-env-staging app-env-prod
```