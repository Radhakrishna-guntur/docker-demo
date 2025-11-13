## Docker Overview

**What is Docker?**

Docker is an open-source platform that automates the deployment, scaling, and management of applications using containerization technology.
It allows developers to package applications and their dependencies into standardized units called containers, which can run
consistently across diﬀerent environments.

**Why do you Need Docker?**

1.One of the primary challenges was ensuring compatibility with the underlying operating system.
Additionally, conflicts between services and their required libraries or dependencies on the OS—where one service needed a particular version of a library and another required a different version.

2.Another significant obstacle was the time-consuming process of setting up development environments for new team members.

3.Different Dev,Test, Staging, Prod Environments.

**Why Use Docker?**

Docker oﬀers numerous advantages for developers and operations teams:

1.Consistency: Ensures applications run the same way in development, testing, and production environments.
2.Isolation: Containers are isolated from each other and the host system, improving security and reducing conflicts.
3.Portability: Containers can run on any system that supports Docker, regardless of the underlying infrastructure.
4.Eﬃciency: Containers share the host system's OS kernel, making them more lightweight than traditional virtual machines.
5.Scalability: Easy to scale applications horizontally by running multiple containers.
6.Version Control: Docker images can be versioned, allowing for easy rollbacks and updates.

**What Are Containers?**

Containers are isolated environments that operate independently from one another. Each container maintains its own processes, network interfaces, and mounts—similar to virtual machines—but all containers share the host OS kernel. Although containerization is not a new concept and has been around for more than a decade, Docker revolutionized it by offering an accessible, user-friendly tool for managing these lightweight LXC containers. While there are other container technologies such as LXC, LXD, and LXCFS, Docker primarily uses LXC containers to simplify management for end users.

**Key Concepts:**

1. Containerization: A lightweight form of virtualization that packages applications and their dependencies together.

2. Docker Engine: The runtime that allows you to build and run containers.

3. Docker Image: A read-only template used to create containers.

4. Docker Container: A runnable instance of a Docker image.

5. Docker Hub: A cloud-based registry for storing and sharing Docker images.

# Simple Web Application

This is a simple web application using [Python Flask](http://flask.pocoo.org/) and [MySQL](https://www.mysql.com/) database. 
This is used in the demonstration of the development of Ansible Playbooks.
  
  Below are the steps required to get this working on a base linux system.
  
  - **Install all required dependencies**
  - **Install and Configure Web Server**
  - **Start Web Server**
   
## 1. Install all required dependencies
  
  Python and its dependencies
  ```bash
  apt-get install -y python3 python3-setuptools python3-dev build-essential python3-pip default-libmysqlclient-dev
  ```
   
## 2. Install and Configure Web Server

Install Python Flask dependency
```bash
pip3 install flask
pip3 install flask-mysql
```

- Copy `app.py` or download it from a source repository
- Configure database credentials and parameters 

## 3. Start Web Server

Start web server
```bash
FLASK_APP=app.py flask run --host=0.0.0.0
```

## 4. Test

Open a browser and go to URL
```
http://<IP>:5000                            => Welcome
http://<IP>:5000/how%20are%20you            => I am good, how about you?
```
