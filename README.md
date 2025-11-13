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

CONTAINER ID           IMAGE                     COMMAND                     CREATED            STATUS                PORTS           NAMES
8e37a3bde73f          nginx:1.14-alpine      "nginx -g 'daemon of…"      4 seconds ago        Up 4 seconds        80/tcp            webapp


**8.Delete all images on the host**

~ ➜  docker rmi $(docker images -aq)
Untagged: mysql:latest
Untagged: mysql@sha256:569c4128dfa625ac2ac62cdd8af588a3a6a60a049d1a8d8f0fac95880ecdbbe5
Deleted: sha256:f6b0ca07d79d7d19c8da64558c3ccdd4ea635ac2193f551a1cb5370f33b494e8
Deleted: sha256:27ef7ea60fab350


**9.Running a Redis Container with Specific Version using Tags:**

docker run redis:4.0


**10.Port Mapping for Containerized Web Applications:**

When running a containerized web application that listens on port 5000, the container’s internal IP (e.g., 172.17.0.2) is only accessible within the Docker host. 

To expose the application externally, you must map a free host port to the container’s port using the -p parameter.

For instance, to route traffic from port 80 on your Docker host to port 5000 in the container, run:


**docker run rk/webapp**

* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)


**docker run -p 80:5000 rk/webapp**

Now, users can access your web application via http://192.168.1.5:80 (assuming 192.168.1.5 is the Docker host IP). You can also run multiple instances of your application by mapping different host ports:

docker run -p 80:5000 rk/webapp

docker run -p 8000:5000 rk/webapp

docker run -p 8001:5000 rk/webapp

For services like MySQL, you may choose to map its default port (3306) or an alternate host port (e.g., 8306) to allow multiple instances to operate concurrently without conflict.


**Note:** In the PORTS column of docker ps, the format is hostPort->containerPort. The value after -> is the container (internal) port.

case:1 Which of the following ports are mapped on the container side (i.e., exposed inside the container)?

80 & 3456

case2: Run an instance of rk/simple-webapp:blue and name the container blue-app, mapping port 8080 on the container to port 38282 on the host

Run the command: **docker run -p 38282:8080 --name blue-app rk/simple-webapp:blue**

**~ ➜  docker run -d --name blue-app -p 38282:8080 rk/simple-webapp:blue**


Unable to find image 'rk/simple-webapp:blue' locally
blue: Pulling from rk/simple-webapp
4fe2ade4980c: Already exists 
7cf6a1d62200: Already exists 
f0d690b9e495: Already exists 
fac5d45ad062: Already exists 
a6fc8a0deb7d: Pull complete 
f43c8e496f88: Pull complete 
58ca939f7651: Pull complete 
095a1a007cdb: Pull complete 
Digest: sha256:9caf15476dc60b77c7460791bea8ea5f6ca02b90199aabe088beea83bc943fe5
Status: Downloaded newer image for rk/simple-webapp:blue
6b28d8833ff3c8c4ae965ee02f7eb6bc6c7b6ee826f607230cbe1c137c18e087




**11.Data Persistence with Docker Volumes:**

By default, a MySQL container stores its data in /var/lib/mysql inside the container. However, since container filesystems are ephemeral, all data is lost when the container is removed. Consider the following example:

docker run mysql   

docker stop mysql    

docker rm mysql  

All stored data is removed along with the container. To persist the data, mount a directory from your Docker host into the container. For example, create a directory /opt/datadir on your host and run:

**docker run -v /opt/datadir:/var/lib/mysql mysql**

This volume mapping ensures that the data in /opt/datadir remains intact even if the container is deleted.

**12.Inspecting Running Containers**

To retrieve basic information about your running containers, use the docker ps command, which lists container names and IDs. For detailed information about a particular container, the docker inspect command provides comprehensive configuration details in JSON format. 

Use docker inspect when you need to review the complete state and configuration of a container.

**13.Viewing Container Logs**

If you launch a container in detached mode using the -d flag, you may want to view its logs later. The docker logs command displays the standard output of a container. 
To view logs from a container named “blissful_hopper,” run:

**docker logs blissful_hopper**


# Docker Images:

How to build your own Docker image:

Custom Docker images are useful when you can't find a specific component on Docker Hub or when containerizing an application for easier deployment and portability is required.

Create a file called Dockerfile and add instructions for setting up your application by installing dependencies, copying the source code, and setting the entrypoint. 
Below is an example Dockerfile:


FROM ubuntu


RUN apt-get update && apt-get install -y python python-pip


RUN pip install flask flask-mysql


COPY . /opt/source-code


ENTRYPOINT ["sh", "-c", "FLASK_APP=/opt/source-code/app.py flask run"]


A Dockerfile is a plain text file defining a series of instructions and arguments that Docker interprets to create an image. Here is an explanation of each instruction used in our example:

**FROM:** Sets the base image—in this case, Ubuntu. Every Dockerfile begins with a FROM instruction referencing an existing image on Docker Hub.

**RUN:** Executes commands in the container. In the Dockerfile, the first RUN command updates the package lists and installs necessary packages. Combining commands with && minimizes the image layers.

**COPY:** Transfers files from your local system into the image. Here, it copies the source code to /opt/source-code.

**ENTRYPOINT:** Specifies the command that runs when the container starts. 
In this example, it sets the environment variable FLASK_APP and starts the Flask web server.

Docker’s layered architecture means that each Dockerfile instruction creates a new layer. For instance:

The base Ubuntu OS.

APT updates and the installation of required packages.

Python package installation.

Copying of the source code.

Setting of the ENTRYPOINT.

Because each layer only adds the differences from the previous one, the final image size only includes these changes. 
You can inspect these layers with the **docker history** command.


<img width="1367" height="710" alt="Screenshot 2025-11-13 at 2 40 30 PM" src="https://github.com/user-attachments/assets/d8b404ad-d343-4c6a-8f34-6b6ba4e71f89" />













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
