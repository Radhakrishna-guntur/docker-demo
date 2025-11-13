## Docker Overview

**What is Docker?**

Docker is an open-source platform that automates the deployment, scaling, and management of applications using containerization technology.
It allows developers to package applications and their dependencies into standardized units called containers, which can run
consistently across diﬀerent environments.

**Why do you Need Docker?**

1.One of the primary challenges was ensuring compatibility with the underlying operating system. Additionally, conflicts between services and their required libraries or dependencies on the OS—where one service needed a particular version of a library and another required a different version.

2.Another significant obstacle was the time-consuming process of setting up development environments for new team members.

3.Different Dev,Test, Staging, Prod Environments.

**Why Use Docker?**

Docker oﬀers numerous advantages for developers and operations teams:

**1.Consistency:** Ensures applications run the same way in development, testing, and production environments.

**2.Isolation:** Containers are isolated from each other and the host system, improving security and reducing conflicts.

**3.Portability:** Containers can run on any system that supports Docker, regardless of the underlying infrastructure.

**4.Eﬃciency:** Containers share the host system's OS kernel, making them more lightweight than traditional virtual machines.

**5.Scalability:** Easy to scale applications horizontally by running multiple containers.

**6.Version Control:** Docker images can be versioned, allowing for easy rollbacks and updates.

**What Are Containers?**

Containers are isolated environments that operate independently from one another. Each container maintains its own processes, network interfaces, and mounts—similar to virtual machines—but all containers share the host OS kernel. Although containerization is not a new concept and has been around for more than a decade, Docker revolutionized it by offering an accessible, user-friendly tool for managing these lightweight LXC containers. While there are other container technologies such as LXC, LXD, and LXCFS, Docker primarily uses LXC containers to simplify management for end users.


# Basic Docker Workflow:

**1.Build:** Create a Dockerfile that defines your application and its dependencies.

**2.Ship:** Push your Docker image to a registry like Docker Hub.

**3.Run:** Pull the image and run it as a container on any Docker-enabled host.

**Here's a simple example of this workflow:**
# Build an image
docker build -t myapp:v1 .
# Ship the image to Docker Hub
docker push username/myapp:v1
# Run the container
docker run -d -p 8080:80 username/myapp:v1


**Key Concepts:**

1. Containerization: A lightweight form of virtualization that packages applications and their dependencies together.

2. Docker Engine: The runtime that allows you to build and run containers.

3. Docker Image: A read-only template used to create containers.

4. Docker Container: A runnable instance of a Docker image.

5. Docker Hub: A cloud-based registry for storing and sharing Docker images.

# Basic Docker Commands

**1. Running a Container:**

The Docker run command creates and starts a container from a specified image. For example, to start an Nginx container, 

simply execute:      # docker run nginx

If the Nginx image already exists on your host, Docker immediately starts a new container. However, if the image is not present, Docker will pull it from Docker Hub.

**2. Listing Containers:**

You can view running containers using the docker ps command. This command provides an overview, including container IDs, image names, statuses, and container names. For instance:

docker ps -a

CONTAINER ID        IMAGE               COMMAND                        CREATED             STATUS                        NAMES
796856ac413d        nginx               "nginx -g 'daemon of..."       7 seconds ago       Up 6 seconds                  silly_sammet
cff8ac918a2f        redis               "docker-entrypoint.s..."       6 seconds ago       Exited (0) 3 seconds ago


To list all containers, including those that have stopped or exited, add the -a flag:

**3.Stopping and Removing Containers**

To stop a running container, provide the container ID or name. First, confirm the container details with:

**docker ps**
Then, stop the container by running:

**docker stop silly_sammet**

After stopping, running docker ps will show no active containers. 

To permanently remove a stopped container, use:

**docker rm silly_sammet**

**docker ps**

The removed container will no longer appear in your Docker listings.

**4. Managing Docker Images:**

Viewing local Docker images is straightforward with the docker images command. This command displays each image along with its size, creation time, and more:

**docker images**

REPOSITORY          TAG       IMAGE ID       CREATED        SIZE
nginx               latest    f68d6e55e065   4 days ago     109MB
redis               latest    4760dc956b2d   15 months ago  107MB
ubuntu              latest    f975c503748    16 months ago  112MB
alpine              latest    3fd9065eaf02   18 months ago  4.14MB


To delete an image no longer needed, ensure no container is using it and execute:

**docker rmi nginx**

Untagged: nginx:latest
Untagged: nginx@sha256:96fb261b66270b900ea5a2c17a26abbfabe95506e73c3a3c65869a6dbe83223a
Deleted: sha256:f68d6e55e06520f152403e69d6d0de5c9790a89b4cf99f4626f68146faldc
Deleted: sha256:1b0c768769e2bb66e74a2531437381a78b77feef8ea6fd7e7f4044e1
Deleted: sha256:34138fb6002a180512485fb96f42e86fbd08c6f1a2506b11ff6b945b03f
Deleted: sha256:cf5b3c6798f77b1f78b297b27cfa5b6caa982f04caeb5de7d13c255fd7ale

5.If you want to download an image for later use without running a container immediately, use the docker pull command:

**docker pull nginx**

Using default tag: latest
latest: Pulling from library/nginx
fc71811084d0: Pull complete
d2e987ca2267: Pull complete
0b760b431b11: Pull complete
Digest: sha256:96fb261b66270b900ea5a2c17a26abbfabe95506e73c3a3c65869a6dbe83223a
Status: Downloaded newer image for nginx:latest

**6.Running Ubuntu Containers**

When using the Ubuntu image, simply running:

**docker run ubuntu**

will start a container that immediately exits. This occurs because Ubuntu, by default, has no long-running process. Check the container status with:

docker ps -a
CONTAINER ID        IMAGE               COMMAND       CREATED             STATUS                      NAMES
45aacca36850        ubuntu              "/bin/bash"   43 seconds ago      Exited (0) 41 seconds ago   <container_name>


To keep the container active, instruct it to run a specific command, such as sleeping for a defined duration:

**docker run ubuntu sleep 5**


Here, the container runs the sleep command for five seconds before exiting.

**7.Running a Web Application Container**

Consider running a simple web application container. For instance, the repository "kodekloud/simple-webapp" contains a sample web application. Running the container in the foreground displays the application's output directly in your terminal:

**docker run -d rk/simple-webapp**

To run the web application in detached (background) mode, add the -d option:

**Example:**  Run a container with the nginx:1.14-alpine image and name it webapp. 

**~ ➜  docker run -d --name webapp nginx:1.14-alpine**

8e37a3bde73f69dc909e655fd19506b9506a4cb5b3dddbdeaa1d1c68fe483601

**~ ➜  docker ps **  

CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS         PORTS     NAMES
8e37a3bde73f   nginx:1.14-alpine   "nginx -g 'daemon of…"   4 seconds ago   Up 4 seconds   80/tcp    webapp

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
