# Hands-On 1: Basic Python App 🐍

This hands-on project demonstrates how to run a basic "Hello, World!" Python script inside a Docker container.  
The setup is done on an **AWS EC2 instance** (Ubuntu OS) with SSH access. It also includes steps for Docker Hub integration.

## 🌐 Prerequisites

- AWS EC2 Ubuntu instance with SSH access
- Docker Hub account (create and verify via email)
- Basic knowledge of terminal and Docker

## ⚙️ Docker Setup on EC2

### 1. Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
```

### 2. Start Docker Daemon

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### 3. Grant Docker Permissions to User

```bash
sudo usermod -aG docker ubuntu
```

> 🔁 Log out and log back in for group changes to take effect.

### 4. Verify Docker Installation

```bash
docker run hello-world
```

## 🐳 Run Your First Dockerized Python App

### 1. Clone the Repository

```bash
git clone https://github.com/DarmilaT/docker-hands-on-examples.git
cd docker-hands-on-examples/hands-on-1-basic-python-app
```

### 2. Login to Docker Hub

#### Option 1: Web-based

```bash
docker login
```

#### Option 2: Username and Password

```bash
docker login -u <your-dockerhub-username>
```

### 3. Build the Docker Image

```bash
docker build -t <your-dockerhub-username>/my-first-docker-image:latest .
```

### 4. Verify the Docker Image

```bash
docker images
```

### 5. Run the Docker Container

```bash
docker run -it <your-dockerhub-username>/my-first-docker-image
```

### 6. Push the Image to Docker Hub

```bash
docker push <your-dockerhub-username>/my-first-docker-image
```

> ✅ Now you can see the image under your Docker Hub repositories

## ✅ Outcome

You’ve successfully:

- Created a Dockerfile for a Python app
- Built a Docker image
- Ran it in a container
- Pushed the image to Docker Hub

This completes your first Docker hands-on exercise! 🎉
