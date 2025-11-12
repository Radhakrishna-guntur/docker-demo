## Docker Overview

**What is Docker?**

Docker is an open-source platform that automates the deployment, scaling, and management of applications using containerization technology.
It allows developers to package applications and their dependencies into standardized units called containers, which can run
consistently across diﬀerent environments.

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
