# Simple Notes App
This is a simple notes app built with React and Django.

## Requirements
1. Python 3.9
2. Node.js
3. React

## Installation
1. Clone the repository
```
git clone https://github.com/LondheShubham153/django-notes-app.git
```

2. Build the app
```
docker build -t notes-app .
```

3. Run the app
```
docker run -d -p 8000:8000 notes-app:latest
```

## Nginx

Install Nginx reverse proxy to make this application available

`sudo apt-get update`
`sudo apt install nginx`

--------------------------------------------------------------------------------------
## Docker Project: Deploying a Django Web Application with Nginx and MySQL on Docker

Dockerization is about creating a portable ecosystem for your application. By combining Django, Nginx, and MySQL in a Docker setup, you ensure scalability,
consistency, and ease of deployment. This guide will walk you through deploying a Django web application with Nginx, MySQL, and Docker Compose.

### Overview of Our Architecture
Here’s what we’ll be deploying:

#### 1. Django Backend: Handles application logic and serves data via APIs.
#### 2. Nginx: Acts as a reverse proxy, improving security and performance.
#### 3. MySQL Database: Stores application data persistently.
#### 4. Docker Compose: Orchestrates these components seamlessly.

### Step 1: Understanding the Dockerfile
Our Dockerfile creates a Docker image for the Django backend. Let’s break it down step-by-step:

```
FROM python:3.9
```
**Base Image:** The official Python 3.9 image provides a preconfigured environment for Python applications, minimizing setup time.

```
WORKDIR /app/backend
```
**Working Directory:** Sets the working directory inside the container to /app/backend. All subsequent commands will execute relative to this directory.

```
COPY requirements.txt /app/backend
```
**Copy Requirements:** Copies the requirements.txt file from your local system to the container. This file lists all the Python dependencies.

```
RUN apt-get update \\\
```
```
   && apt-get upgrade -y \\\\
```
```
    && apt-get install -y gcc default-libmysqlclient-dev pkg-config \\\\
```
```
    && rm -rf /var/lib/apt/lists/ 
```
**Install System Dependencies:** gcc: A compiler required for building some Python packages. default-libmysqlclient-dev: MySQL development headers for compatibility with mysqlclient. pkg-config: Ensures smooth installation of dependencies. rm -rf /var/lib/apt/lists/*: Cleans up to reduce image size.

```
RUN pip install mysqlclient
```
```
RUN pip install --no-cache-dir -r requirements.txt
```
**Install Python Dependencies:** mysqlclient: Enables Django to interact with MySQL. Other dependencies are installed from requirements.txt.

```
COPY . /app/backend
```
**Copy Application Code:** Copies all files from your local backend directory to the container’s working directory.

```EXPOSE 8000```
**Expose Port:** Makes port 8000 available for communication with the host machine.

This Dockerfile creates an isolated, dependency-ready environment for running your Django app.
             

