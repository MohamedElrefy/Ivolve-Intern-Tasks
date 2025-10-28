# 🧪 Lab 10: Multi-Stage Build for a Node.js App

## 📘 Objective
In this lab, we will build a Java-based Node.js application using a **multi-stage Docker build**.  
This approach helps reduce the final image size by separating the **build stage** from the **runtime stage**.

## 1️⃣ Create a Multi-Stage Dockerfile
This Dockerfile uses a multi-stage build to make the final image smaller and more efficient.
It’s divided into two stages: a build stage and a runtime stage.

### 🏗️ 1. Build Stage

Uses a Maven base image that already includes Java.

Copies the application source code into the container.

Runs mvn package to compile and build the application.

The result is a JAR file created inside the target/ directory.

### 🚀 2. Runtime Stage

Uses a lightweight Java image (based on Alpine Linux) for running the app.

Copies only the JAR file from the first stage — not the entire source code.

Exposes port 8080 so the app can receive traffic.

Runs the application using the java -jar command.

## 2️⃣  Build the Docker Image

Build the Docker image and name it app3:
```bash
docker build -t app3 .
```
## 3️⃣ Run the Container

Run the application container:
```bash
docker run -d -p 8080:8080 --name app3-container app3
```
## 4️⃣ Test the Application
```bash
curl http://localhost:8080
```