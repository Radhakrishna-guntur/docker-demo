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

**1. Containerization:** A lightweight form of virtualization that packages applications and their dependencies together.

**2. Docker Engine:** The runtime that allows you to build and run containers.

**3. Docker Image:** A read-only template used to create containers.

**4. Docker Container:** A runnable instance of a Docker image.

**5. Docker Hub:** A cloud-based registry for storing and sharing Docker images.

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

**5.Pull Image**

If you want to download an image for later use without running a container immediately, use the docker pull command:

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

**docker ps -a**


CONTAINER ID        IMAGE               COMMAND       CREATED             STATUS                      NAMES
45aacca36850        ubuntu              "/bin/bash"   43 seconds ago      Exited (0) 41 seconds ago   <container_name>


To keep the container active, instruct it to run a specific command, such as sleeping for a defined duration:


**docker run ubuntu sleep 5**


Here, the container runs the sleep command for five seconds before exiting.

**7.Running a Web Application Container**

Consider running a simple web application container. For instance, the repository "rk/simple-webapp" contains a sample web application. Running the container in the foreground displays the application's output directly in your terminal:

**docker run -d rk/simple-webapp**

To run the web application in detached (background) mode, add the -d option:

**Example:**  Run a container with the nginx:1.14-alpine image and name it webapp. 

**~ ➜  docker run -d --name webapp nginx:1.14-alpine**


8e37a3bde73f69dc909e655fd19506b9506a4cb5b3dddbdeaa1d1c68fe483601


**~ ➜  docker ps**


CONTAINER ID           IMAGE                     COMMAND                     CREATED            STATUS                PORTS           NAMES
8e37a3bde73f          nginx:1.14-alpine      "nginx -g 'daemon of…"      4 seconds ago        Up 4 seconds        80/tcp            webapp


**8.Delete all Container and  images on the host**


**First Stop and delete all the containers being used by images.**

**~ ➜  docker stop $(docker ps -aq)**

f397836ced8e

**~ ✖ docker rm $(docker ps -aq)**     

f397836ced8e

**Then run the command to delete all the available images:** 

**docker rmi $(docker images -aq)**

~ ➜  docker rmi $(docker images -aq)


Untagged: mysql:latest
Untagged: mysql@sha256:569c4128dfa625ac2ac62cdd8af588a3a6a60a049d1a8d8f0fac95880ecdbbe5
Deleted: sha256:f6b0ca07d79d7d19c8da64558c3ccdd4ea635ac2193f551a1cb5370f33b494e8
Deleted: sha256:27ef7ea60fab350


**9.Running a Redis Container with Specific Version using Tags:**

**docker run redis:4.0**


**10.Port Mapping for Containerized Web Applications:**


When running a containerized web application that listens on port 5000, the container’s internal IP (e.g., 172.17.0.2) is only accessible within the Docker host. 

To expose the application externally, you must map a free host port to the container’s port using the ** -p ** parameter.

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

Run the command:

**docker run -p 38282:8080 --name blue-app rk/simple-webapp:blue**

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


<img width="1440" height="900" alt="Screenshot 2025-11-26 at 11 12 07 AM" src="https://github.com/user-attachments/assets/3d86adb8-2361-4fba-84e6-98139d9e8c41" />

NOte: pics ate capture from Mumshad course for better understanding the topics.

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



**Demo Creating a new Docker Image:**

**Step1:** Creating a Dockerfile to build a custom image.

**Step2:** Building, running, and verifying the Docker image.

**Step3:** Tagging and pushing the image to Docker Hub for public distribution.


## Dockerizing the Application

After verifying your web application inside a Docker container, you can now create a Docker image.

**Creating a Dockerfile**

Create a project directory (e.g., my-simple-webapp) and add a file named Dockerfile with the following content:

FROM ubuntu

Update package lists and install Python and pip

RUN apt-get update && apt-get install -y python python-pip

Install Flask via pip

RUN pip install flask

Copy application source code into the container

COPY app.py /opt/app.py

Set the entrypoint to run the Flask application

ENTRYPOINT ["flask", "run", "--host=0.0.0.0", "--app", "/opt/app.py"]

Ensure that your app.py file is in the same directory as your Dockerfile.


**Building the Image**

Build your Docker image by running:

**docker build . -t my-simple-webapp**


Docker caches each layer, so subsequent builds without changes will be faster. To verify the image was built, list your Docker images:

**docker images**

Your image my-simple-webapp should appear in the list.

**Running the Docker Image**

To run your containerized application, execute:

**docker run my-simple-webapp**

Without port mapping, the application is accessible only from the host or via Docker’s internal IP. To make the application accessible externally, run:

**docker run -p 5000:5000 my-simple-webapp**

Then, navigate to http://<HOST_IP>:5000 in your web browser.

**Pushing the Image to Docker Hub**

Sharing your application on Docker Hub is simple. Follow these steps:

**1.Tag your image using your Docker Hub username (e.g., if your username is rguntur):**

docker build . -t rguntur/my-simple-webapp

**2.Log in to Docker Hub:**

docker login

Enter your username and password when prompted.

**3.Push the image to Docker Hub:**

docker push rguntur/my-simple-webapp

If you encounter an error like “requested access to the resource is denied,” ensure that you have tagged your image with your Docker Hub account name and that you are logged in.

Upon a successful push, your image will be available in your Docker Hub repository. You can view it on your Docker Hub dashboard.


**4.Others can pull your image by running:**

docker pull mmumshad/my-simple-webapp


**Dockerfile Instructions**


**1.FROM : The FROM instruction initializes a new build stage and sets the base image for subsequent instructions.**

FROM ubuntu:20.04

This instruction is typically the first one in a Dockerfile. It's possible to have multiple FROM instructions in a single Dockerfile for multi-stage builds.

**2.LABEL: LABEL adds metadata to an image in key-value pair format.** 

LABEL version="1.0" maintainer="john@example.com"

description="This is a sample Docker image"

Labels are useful for image organization, licensing information, annotations, and other metadata.

**3.ENV: ENV sets environment variables in the image.**

ENV APP_HOME=/app NODE_ENV=production

These variables persist when a container is run from the resulting 70 image.

**4.WORKDIR: WORKDIR sets the working directory for any subsequent RUN, CMD, ENTRYPOINT, COPY, and ADD instructions.**

WORKDIR /app : If the directory doesn't exist, it will be created.

**5.COPY and ADD : Both COPY and ADD instructions copy files from the host into the image.**

COPY package.json .

ADD https://example.com/big.tar.xz /usr/src/things/

COPY is generally preferred for its simplicity. ADD has some extra features like tar extraction and remote URL support, but these can make build behavior less predictable.

**6. RUN : RUN executes commands in a new layer on top of the current image and commits the results.**

RUN apt-get update && apt-get install -y nodejs

It's a best practice to chain commands with && and clean up in the same RUN instruction to keep layers small.

**7. CMD : CMD provides defaults for an executing container. There can only be one**

CMD instruction in a Dockerfile.

CMD ["node", "app.js"]

CMD can be overridden at runtime.

**8.ENTRYPOINT: ENTRYPOINT configures a container that will run as an executable.**

ENTRYPOINT ["nginx", "-g", "daemon off;"]

ENTRYPOINT is often used in combination with CMD, where ENTRYPOINT defines the executable and CMD supplies default arguments.

**9. EXPOSE informs Docker that the container listens on specified network ports at runtime.**

EXPOSE 80 443

This doesn't actually publish the port; it functions as documentation between the person who builds the image and the person who runs the container.

**10. VOLUME: VOLUME creates a mount point and marks it as holding externally mounted volumes from native host or other containers.**

VOLUME /data

This is useful for any mutable and/or user-serviceable parts of your image.

**11. ARG : ARG defines a variable that users can pass at build-time to the builder with the docker build command.**

ARG VERSION=latest

This allows for more flexible image builds.




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


Practice these steps to master Docker containerization and share your applications with the community. Happy containerizing!


## Docker Compose:

Docker Compose is a tool used for defining and running multi-container Docker applications. It simplifies the management of complex applications that consist of multiple interconnected services, each running in its own Docker container. 

**Primary uses of Docker Compose include:**

**Defining Multi-Container Applications:** Compose uses a YAML file (typically docker-compose.yml) to define all the services that constitute an application.

This file specifies details like the Docker images to use, port mappings, volume mounts, environment variables, dependencies between services, and network configurations.

**Orchestrating Service Lifecycle:** With a single command, docker compose up, Compose can build (if necessary), create, and start all the services defined in the docker-compose.yml file.

Similarly, docker compose down can stop and remove all associated containers, networks, and volumes.

**Simplifying Development Workflows:** Developers can define their entire application stack in a docker-compose.yml file, making it easy to share and reproduce development environments. 

This allows team members to quickly set up and run the application with consistent configurations.

**Managing Dependencies and Order:** Compose understands service dependencies and can start services in the correct order, ensuring that, for example, a database service is running before an application service attempts to connect to it.


**Streamlining Configuration:** Instead of manually running multiple docker run commands with complex arguments, Compose provides a declarative way to specify all container configurations in a single, human-readable file.


In essence, Docker Compose acts as an orchestration tool for local development and testing environments, making it significantly easier to manage and interact with multi-container Docker applications.

## Sample Docker Compose File:


<img width="598" height="701" alt="Screenshot 2025-11-26 at 3 09 58 PM" src="https://github.com/user-attachments/assets/cc571f15-edc8-4937-a176-bd3e66b4dbde" />



**Configuring Networks in Docker Compose**

Docker Compose lets you define custom networks to control traffic between services. For instance, you might separate external (user-facing) traffic from internal (service-to-service) communication.

**Example: Defining Separate Networks**

This example configuration connects the voting and results applications to both the front-end (user traffic) and back-end (internal services) networks, while Redis and PostgreSQL are only accessible on the back-end network.



<img width="643" height="667" alt="Screenshot 2025-11-26 at 3 04 17 PM" src="https://github.com/user-attachments/assets/b6790b9f-82fe-4049-ab83-54917fef6810" />

    
  
This configuration ensures that internal data remains secure while still allowing user access to essential services.


**Use Dry Run mode to test your command**

Use --dry-run flag to test a command without changing your application stack state. Dry Run mode shows you all the steps Compose applies when executing a command, for example:

  
 docker compose --dry-run up --build -d
[+] Pulling 1/1
 ✔ DRY-RUN MODE -  db Pulled                                                                                                                                                                                                               0.9s
[+] Running 10/8
 ✔ DRY-RUN MODE -    build service backend                                                                                                                                                                                                 0.0s
 ✔ DRY-RUN MODE -  ==> ==> writing image dryRun-754a08ddf8bcb1cf22f310f09206dd783d42f7dd        


 **Docker Engine:** 

 Docker Engine is the core component of the Docker platform, providing the runtime environment for containers. It is an open-source client-server application that enables users to build, run, and manage containerized applications.
 
**Key components of Docker Engine:**

**Docker Daemon (dockerd):** This is a long-running background process that runs on the host machine. It manages Docker objects such as images, containers, networks, and volumes. The daemon listens for API requests and performs the necessary actions to build, run, and monitor containers.

**REST API:** This specifies the interfaces that programs and the Docker CLI use to communicate with and instruct the Docker Daemon.

**Docker CLI (Command Line Interface):** This is the primary way users interact with Docker Engine. Users issue docker commands through the CLI, which then uses the REST API to send instructions to the Docker Daemon.

**How it works:**

When a user issues a command like docker run via the CLI, the command is sent to the Docker Daemon through the REST API.
The Docker Daemon then takes this instruction and performs the necessary actions, such as pulling a Docker image, creating a container from that image, and running the application within the container.

The Docker Engine ensures that containers are isolated from each other and bundle their own software, libraries, and configuration files, allowing them to run consistently across different environments.


<img width="793" height="568" alt="image" src="https://github.com/user-attachments/assets/117ebf98-364b-42f8-a8e4-f1b7358d97cc" />


## How Containers Isolate Applications:

Docker leverages Linux namespaces to isolate various system resources including:

**Workspaces**

**Process IDs**

**Network interfaces**

**Inter-process communication (IPC)**

**Filesystem mounts**

**Unix time-sharing systems**

This isolation provides containers with the appearance of independent systems while sharing hardware resources with the host.

**Managing Resources with cgroups**:

Containers by default can use as much resource as they require, which may lead to resource exhaustion on the host. Docker utilizes Linux control groups (cgroups) to constrain the hardware resources available to each container, ensuring efficient resource management.

You can limit resource usage by employing options such as --cpus and --memory. For instance, to restrict a container to using only 50% of the host CPU and 100 megabytes of memory, run:

**docker run --cpus=0.5 ubuntu**

**docker run --memory=100m ubuntu**

# Docker Storage

**Docker's File Storage Architecture**:

When Docker is installed, it establishes a directory structure typically at /var/lib/docker. This root directory contains several subdirectories that serve different purposes:

**containers:** Stores files related to running containers.

**images:** Contains image-related files.

**volumes:** Holds data for Docker volumes.

**overlay2:** Manages the overlay filesystem for layering.



**Docker's Layered Architecture**:

Docker images are constructed using a layered approach. Each instruction in a Dockerfile creates a distinct layer that only contains changes from the previous layer. 

For example, consider the following Dockerfile:

FROM ubuntu

RUN apt-get update && apt-get -y install python

RUN pip install flask flask-mysql

COPY . /opt/source-code

ENTRYPOINT ["flask", "run"]


**Build the image using:**

**docker build -t rk/my-custom-app** 


**In this Dockerfile:**

**Base Image:** The first layer pulls the Ubuntu base image.

**APT Packages:** The second layer installs necessary APT packages.

**Python Packages:** The third layer installs Python packages required by the application.

**Source Code:** The fourth layer copies your application code into the container.

**Entrypoint:** The final layer sets the container's entry point.

Because each layer contains only the incremental changes, their sizes reflect only the modifications from the previous layer. 
For instance, even if the base Ubuntu image is large, layers that add extra packages or code remain relatively small.



<img width="1382" height="764" alt="Screenshot 2025-11-26 at 11 27 05 AM" src="https://github.com/user-attachments/assets/05e941f2-9ce7-4c63-9445-6cca68a63b3b" />



<img width="1440" height="900" alt="Screenshot 2025-11-26 at 11 12 07 AM" src="https://github.com/user-attachments/assets/f0b8124f-e80c-444f-a979-8d772929b622" />



**Docker Storage Drivers**:

Docker storage drivers manage the layered filesystem, create writable layers, and implement the copy-on-write mechanism. Popular storage drivers include AUFS, VTRFS, VFS, Device Mapper, Overlay, and Overlay2. 

The default driver is determined by your operating system and kernel support. For instance, modern Ubuntu installations often use Overlay2, while Fedora or CentOS might use Device Mapper.

Each driver offers different performance and stability characteristics, so it’s essential to choose the one that best meets your application needs. 

