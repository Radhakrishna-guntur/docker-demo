# What is Docker?

Docker is an OS‑level virtualization (or containerization) platform, which allows applications to share the host OS kernel instead of running a separate guest OS like in traditional virtualization. This design makes Docker containers lightweight, fast, and portable, while keeping them isolated from one another.

# Written in the Go programming language.

Supports Windows, macOS, and Linux installations (Docker Engine runs natively on Linux).
Solves the “works on my machine” problem by ensuring code runs identically across environments.
Unlike VMware (hardware‑level virtualization), Docker operates at the OS level.

**Before Docker:**

Deploying applications across environments was often difficult, dependencies, configs, and OS variations caused “works here but not there” headaches.

<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/afcfddba-d34f-40ac-b019-e1280deec9fb" />


**dockervsvm**

Docker’s Solution:

Standardizes the runtime environment by bundling everything (app + dependencies) into containers.


**Portability:** Runs anywhere in local machine, cloud, on‑prem servers.

**Consistency:** Same behavior in development, testing, and production.

**Lightweight:** No full OS per app; containers share the host kernel.

**Scalability:** Ideal for microservices and orchestrators like Kubernetes and Docker Swarm.

**Efficiency:** Starts in seconds, uses fewer system resources.

Understanding Docker's core concepts is essential, but practical experience is what truly sets you apart. Platforms like Hostinger make it easy to deploy Docker containers, allowing you to focus on developing and testing your applications. Hostinger's scalable infrastructure provides an ideal environment for learning and experimenting with Docker in a real-world setting. Their seamless integrationwith Docker containers ensures that whether you're running simple apps or complex multi-container setups, you can deploy with ease.

## Components of Docker

**The following are the some of the key components of Docker:**

## Docker Engine: 
Docker Engine has a core part docker daemon , that handles the creation and management of containers.

## Docker Image:
Docker Image is a read-only template that is used for creating containers, containing the application code and dependencies.

## Docker Hub: 
It is a cloud based repository that is used for finding and sharing the container images.

## Dockerfile:
It is a file that describes the steps to create an image quickly.

## Docker Registry :
It is a storage distribution system for docker images, where you can store the images in both public and private modes.

## Docker Engine

The Docker Engine is the core component that enables Docker to run containers on a system. It follows a client-server architecture and is responsible for building, running, and managing Docker containers.

The Docker Engine Daemon (dockerd) runs in the background, listening to API requests and managing objects like images, containers, networks, and volumes.
The Docker Client (docker CLI) communicates with the daemon using a REST API. It provides the execution environment where Docker Images are instantiated into live containers.
docengine


<img width="793" height="568" alt="image" src="https://github.com/user-attachments/assets/454517bb-bfba-459b-89fe-cff9b43d6410" />


Without the Docker Engine, Docker images cannot be built or containers executed.

The Client sends Docker commands (docker build, docker run, etc.).
The Daemon receives these commands and performs container operations.
The REST API is the interface enabling this communication.
In short, the Docker Engine is the runtime that makes containerization possible by connecting the Docker client with the daemon to build and manage containers efficiently.

## Dockerfile
The Dockerfile uses DSL (Domain Specific Language) and contains instructions for generating a Docker image. Dockerfile will define the processes to quickly produce an image. While creating your application, you should create a Dockerfile in order since the Docker daemon runs all of the instructions from top to bottom.

The Dockerfile is the source code of the image.

(The Docker daemon, often referred to simply as "Docker," is a background service that manages Docker containers on a system.)

It is a text document that contains necessary commands which on execution help assemble a Docker Image.

Docker image is created using a Dockerfile.

<img width="1000" height="362" alt="image" src="https://github.com/user-attachments/assets/c6ebdd67-dfe6-4973-81a5-149d53cea7a6" />



Dockerfile

Docker Image

Docker Architecture and Working

Docker makes use of a client-server architecture. The Docker client talks with the docker daemon which helps in building, running, and distributing the docker containers. The Docker client runs with the daemon on the same system or we can connect the Docker client with the Docker daemon remotely. With the help of REST API over a UNIX socket or a network, the docker client and daemon interact with each other. To know more about working of docker refer to the Architecture of Docker .

Docker Architecture

<img width="1000" height="382" alt="image" src="https://github.com/user-attachments/assets/51d82b20-d596-4ef1-b1c4-be0f55ca5d48" />


## Docker CLI
Command-line interface to interact with Docker
Common commands: docker run, docker build, docker pull
## Docker Rest API
HTTP API used by the CLI and other tools
Facilitates communication with the Docker daemon
## Docker Daemon
Handles images, containers, networks, and volume
Core service that manages Docker objects
High-Level Runtime
Manages container lifecycle operations
Tasks include create, start, stop, and delete containers

## Docker Image
A Docker Image is a file made up of multiple layers that contains the instructions to build and run a Docker container. t acts as an executable package that includes everything needed to run an application — code, runtime, libraries, environment variables, and configurations.

**How it Works:**

The image defines how a container should be created.
Specifies which software components will run and how they are configured.
Once an image is run, it becomes a Docker Container.
Relation to Containers:

##  Docker Image → Blueprint (static, read-only).

## Docker Container → Running instance of that image (dynamic, executable)


## Docker Container
A Docker Container is a lightweight, runnable instance of a Docker Image. It packages the application code together with all its dependencies and runs it in an isolated environment. Containers allow applications to run quickly and consistently across different environments — whether on a developer’s laptop, test servers, or production.

A container is created when a Docker Image is executed.
It runs as an isolated process on the host machine but shares the host’s operating system kernel.
Multiple containers can run on the same system without interfering with each other.
For eg - Suppose there is an image of Ubuntu OS with NGINX SERVER when this image is run with the docker run command, then a container will be created and NGINX SERVER will be running on Ubuntu OS. 

**Relation to Images:**

## Docker Image = Blueprint (static, read-only).
## Docker Container = Live instance of that blueprint (dynamic, executable)


## What is Docker Hub?

Docker Hub is a repository service and it is a cloud-based service where people push their Docker Container Images and also pull the Docker Container Images from the Docker Hub anytime or anywhere via the internet.

## Dockerhub:

Generally it makes it easy to find and reuse images. It provides features such as you can push your images as private or public registry where you can store and share Docker images.

<img width="1000" height="546" alt="image" src="https://github.com/user-attachments/assets/520da953-d68b-4a1d-8a68-9b37cca607e6" />


Mainly DevOps team uses the Docker Hub. It is an open-source tool and freely available for all operating systems. It is like storage where we store the images and pull the images when it is required. When a person wants to push/pull images from the Docker Hub they must have a basic knowledge of Docker. Let us discuss the requirements of the Docker tool.

## Docker Commands:

Through introducing the essential docker commands, docker became a powerful software in streamlining the container management process. It helps in ensuring a seamless development and deployment workflows. The following are the some of docker commands that are used commonly:

**Docker Run:** It used for launching the containers from images, with specifying the runtime options and commands.
**Docker Pull:** It fetches the container images from the container registry like Docker Hub to the local machine.
**Docker ps :** It helps in displaying the running containers along with their important information like container ID, image used and status.
**Docker Stop :** It helps in halting the running containers gracefully shutting down the processes within them.
**Docker Start:** It helps in restarting the stopped containers, resuming their operations from the previous state.
**Docker Login:** It helps to login in to the docker registry enabling the access to private repositories.

## Docker Engine
The software that hosts the containers is named Docker Engine. Docker Engine is a client-server based application. The docker engine has 3 main components:

Server: It is responsible for creating and managing Docker images, containers, networks, and volumes on the Docker. It is referred to as a daemon process.
REST API : It specifies how the applications can interact with the Server and instructs it what to do.
Client: The Client is a docker command-line interface (CLI), that allows us to interact with Docker using the docker commands.
Docker has two Editions:
Community Edition (CE): Free, open‑source, used by individuals, dev teams, open‑source contributors.
Enterprise Edition (EE): Paid, with security enhancements, certified plugins/images, and enterprise support.

Reference Links: 

https://www.geeksforgeeks.org/devops/introduction-to-docker/

https://www.geeksforgeeks.org/devops/docker-instruction-commands/
