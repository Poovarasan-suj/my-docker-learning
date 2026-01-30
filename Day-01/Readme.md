# Docker Basics – Beginner Friendly Guide

## 1. Introduction

This document is a beginner‑friendly guide based on hands‑on practice. It explains **what Docker is, why it is used, and how to work with Docker images and containers** in a simple and practical way. 
---

## 2. What is Docker?

Docker is a **containerization platform** that allows us to package an application along with its libraries, dependencies, and configuration into a single unit called a **container**.

Key points:

* Docker helps applications run **the same way everywhere**
* It avoids dependency and environment issues
* It is lightweight and fast

In simple words:

> Docker helps us build once and run anywhere.

---

## 3. Why Docker is Used in IT Environments

### Problems before Docker:

* Applications worked on one system but failed on another
* Dependency conflicts between applications
* Virtual Machines consumed too much disk, RAM, and CPU
* Scaling applications was slow

### How Docker solves these problems:

* Packages app + dependencies together
* Uses fewer resources
* Starts containers in seconds
* Makes deployments consistent and portable

---

## 4. Docker vs Virtual Machines (VM)

### Virtual Machine (VM):

* Each VM has a **full operating system**
* Heavy disk usage (10–20 GB per VM)
* Slow boot time (minutes)
* Lower resource efficiency

### Docker Containers:

* Containers **do not have their own OS**
* Share the **host OS kernel**
* Lightweight (MBs instead of GBs)
* Start in seconds

### Simple comparison:

| Feature        | VM      | Docker  |
| -------------- | ------- | ------- |
| Guest OS       | Yes     | No      |
| Startup time   | Minutes | Seconds |
| Resource usage | High    | Low     |
| Portability    | Medium  | High    |

---

## 5. What is a Docker Image?

A Docker image is a **blueprint or template** used to create containers.

Important points:

* Image is **read‑only**
* Image is **not running**
* One image can create many containers

Example:

* `nginx` image
* `httpd` image

---

## 6. What is a Docker Container?

A Docker container is a **running instance of a Docker image**.

Key points:

* Container is **live and running**
* It runs the actual application
* Containers can be started, stopped, and deleted

Think like this:

> Image = Blueprint
> Container = Running application

---

## 7. Basic Docker Image Commands

* List images:

  ```bash
  docker images
  ```

* Download an image:

  ```bash
  docker pull nginx
  ```

* Build an image from Dockerfile:

  ```bash
  docker build -t myapp .
  ```

* Remove an image:

  ```bash
  docker rmi nginx
  ```

---

## 8. Creating a Docker Container

To create and run a container:

```bash
docker run -itd --name mycontainer -p 8080:80 nginx
```

Explanation:

* `-d` → run in background
* `-p` → publish port (host:container)
* `--name` → custom container name

---

## 9. Port Publishing (Accessing Application)

Port publishing allows access to the container application from outside.

Example:

```bash
docker run -p 8082:80 httpd
```

Access using:

```
http://<EC2-PUBLIC-IP>:8082
```

---

## 10. Logging into a Docker Container

To enter inside a running container:

```bash
docker exec -it <container-id> /bin/bash
```

Inside the container you can:

* Run Linux commands
* Check OS details
* Modify application files

Exit safely using:

```bash
exit
```

---

## 11. Modifying Containers

Containers are **temporary by nature**.

Best practice:

* Stop container
* Remove container
* Recreate container with new settings

Example:

* Change port
* Change name
* Change image

---

## 12. Container Management Commands

* List running containers:

  ```bash
  docker ps
  ```

* List all containers:

  ```bash
  docker ps -a
  ```

* Stop a container:

  ```bash
  docker stop <container-id>
  ```

* Start a container:

  ```bash
  docker start <container-id>
  ```

* Remove a container:

  ```bash
  docker rm <container-id>
  ```

