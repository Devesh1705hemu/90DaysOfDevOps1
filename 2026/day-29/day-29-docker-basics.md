# Day 29 Docker_Basics
## Task 1: What is Docker?

### Q1. What is a Container and Why Do We Need Them?

**Answer:**

A container is a lightweight, isolated environment that packages an application along with its dependencies, libraries, and configuration.

### Why do we need containers?

* Provides a consistent environment.
* Makes applications portable.
* Isolates applications from each other.
* Uses fewer resources than virtual machines.
* Starts quickly.
* Makes deployment and scaling easier.

**Example:**

```text
Application + Dependencies → Container
```

---

## Q2. Containers vs Virtual Machines: What's the Real Difference?

**Answer:**

The main difference is that **containers share the host OS kernel**, while **virtual machines have their own guest operating system**.

| Containers                  | Virtual Machines        |
| --------------------------- | ----------------------- |
| Share host OS kernel        | Have their own guest OS |
| Lightweight                 | Heavy                   |
| Start quickly               | Start slower            |
| Use fewer resources         | Use more resources      |
| Application-level isolation | Full OS virtualization  |

**Simple example:**

```text
Virtual Machine:
Hardware → Hypervisor → Guest OS → Application

Container:
Hardware → Host OS → Container → Application
```

---

## Q3. What is Docker Architecture?

**Answer:**

Docker follows a **client-server architecture**. The main components are:

### 1. Docker Client

The Docker Client is used to interact with Docker through commands.

```bash
docker run
docker build
docker ps
docker pull
```

### 2. Docker Daemon

The Docker Daemon (`dockerd`) runs in the background and manages Docker objects such as containers, images, networks, and volumes.

### 3. Docker Image

A Docker image is a read-only template used to create containers.

```text
Docker Image → Docker Container
```

### 4. Docker Container

A container is a running instance of a Docker image.

### 5. Docker Registry

A registry stores and distributes Docker images.

**Example:** Docker Hub

---

## Q4. Describe the Docker Architecture in Your Own Words

**Answer:**

Docker works like a client-server system. We give commands through the **Docker Client**, which communicates with the **Docker Daemon**. The daemon manages Docker images and containers.

```text
                 Docker Registry
                    Docker Hub
                       ↕
                    Pull/Push
                       ↕
              ┌─────────────────┐
              │  Docker Client  │
              └────────┬────────┘
                       ↓
              ┌─────────────────┐
              │ Docker Daemon   │
              │    dockerd      │
              └────────┬────────┘
                       ↓
              ┌─────────────────┐
              │  Docker Image   │
              └────────┬────────┘
                       ↓
              ┌─────────────────┐
              │ Docker Container │
              └────────┬────────┘
                       ↓
                 Running App
```

### Simple Flow

```text
Dockerfile
    ↓
Docker Image
    ↓
Docker Container
    ↓
Running Application
```

## Task 2: Install Docker

### Q1. How do you install Docker?

**Answer:**

Docker can be installed on a local machine or a cloud instance such as an AWS EC2 Ubuntu server.

After installation, Docker can be verified using:

```bash
docker --version
```

To check whether the Docker service is running:

```bash
sudo systemctl status docker
```

---

### Q2. How do you verify the Docker installation?

**Answer:**

Run:

```bash
docker --version
```

Example:

```text
Docker version 29.x.x
```

We can also check Docker information using:

```bash
docker info
```

---

### Q3. How do you run the `hello-world` container?

**Answer:**

Run:

```bash
docker run hello-world
```

Docker checks whether the `hello-world` image is available locally. If it is not available, Docker pulls it from Docker Hub, creates a container from the image, runs it, and displays the output.

To check the container afterward:

```bash
docker ps -a
```

The container will normally show as **Exited** because `hello-world` runs once and then stops.

---

### Q4. What happens when you run `docker run hello-world`?

**Answer:**

The basic flow is:

```text
docker run hello-world
        ↓
Check image locally
        ↓
Pull image if not available
        ↓
Create container
        ↓
Start container
        ↓
Display Hello from Docker!
        ↓
Container exits
```

This demonstrates the basic Docker workflow of **image → container → application**.

---

# Task 3: Run Real Containers

## Q1. How do you run an Nginx container and access it in a browser?

**Answer:**

Run:

```bash
docker run -d -p 80:80 --name nginx-server nginx
```

Here:

```text
-d              → Run in detached mode
-p 80:80        → Host port 80 → Container port 80
--name          → Give the container a custom name
nginx           → Docker image
```

Check the container:

```bash
docker ps
```

Then access Nginx using:

```text
http://EC2-PUBLIC-IP
```

If using AWS EC2, make sure port **80** is allowed in the Security Group.

---

## Q2. How do you run an Ubuntu container in interactive mode?

**Answer:**

Run:

```bash
docker run -it --name ubuntu-practice ubuntu /bin/bash
```

Now we can interact with the Ubuntu container like a small Linux machine.

Try:

```bash
whoami
pwd
ls /
cat /etc/os-release
```

Create and explore files:

```bash
mkdir devops
cd devops
touch test.txt
echo "Hello Docker" > test.txt
cat test.txt
```

Exit the container using:

```bash
exit
```

---

## Q3. How do you list all running containers?

**Answer:**

Use:

```bash
docker ps
```

This shows only currently running containers.

---

## Q4. How do you list all containers, including stopped ones?

**Answer:**

Use:

```bash
docker ps -a
```

This displays both running and stopped containers.

---

## Q5. How do you stop and remove a container?

**Answer:**

First, find the container:

```bash
docker ps
```

Stop it:

```bash
docker stop nginx-server
```

Remove it:

```bash
docker rm nginx-server
```

We can also force remove a running container:

```bash
docker rm -f nginx-server
```

---

# Task 4: Explore

## Q1. What is detached mode?

**Answer:**

Detached mode runs a container in the background.

Use:

```bash
docker run -d nginx
```

The terminal remains available instead of attaching to the container's output.

Check the running container:

```bash
docker ps
```

Without `-d`, the terminal can remain attached to the container process.

---

## Q2. How do you give a container a custom name?

**Answer:**

Use the `--name` option:

```bash
docker run -d --name my-nginx nginx
```

Now we can manage the container using:

```bash
docker stop my-nginx
docker start my-nginx
docker logs my-nginx
docker rm my-nginx
```

---

## Q3. How do you map a port from the container to the host?

**Answer:**

Use the `-p` option:

```bash
docker run -d -p 8080:80 --name my-nginx nginx
```

The format is:

```text
-p HOST_PORT:CONTAINER_PORT
```

So:

```text
Host:      8080
              ↓
Container:   80
```

We can access Nginx using:

```text
http://EC2-PUBLIC-IP:8080
```

---

## Q4. How do you check the logs of a running container?

**Answer:**

Use:

```bash
docker logs my-nginx
```

To continuously follow the logs:

```bash
docker logs -f my-nginx
```

`-f` means **follow**, so new log output will appear in real time.

---

## Q5. How do you run a command inside a running container?

**Answer:**

Use `docker exec`.

For example, to open a Bash shell:

```bash
docker exec -it my-nginx /bin/bash
```

If Bash is not available, use:

```bash
docker exec -it my-nginx /bin/sh
```

You can then run commands inside the container:

```bash
pwd
ls
whoami
```

Exit using:

```bash
exit
```

---

# Docker Commands Practiced

```bash
docker --version
docker info
docker run hello-world

docker run -d -p 80:80 --name nginx-server nginx
docker run -it --name ubuntu-practice ubuntu /bin/bash

docker ps
docker ps -a

docker stop nginx-server
docker rm nginx-server

docker run -d nginx
docker run -d --name my-nginx nginx
docker run -d -p 8080:80 --name my-nginx nginx

docker logs my-nginx
docker logs -f my-nginx

docker exec -it my-nginx /bin/bash
```

## Key Docker Concepts

```text
Docker Image
     ↓
docker run
     ↓
Docker Container
     ↓
Running Application
```

```text
Docker Client
      ↓
Docker Daemon
      ↓
Images / Containers / Networks / Volumes
```

### Important Options

| Option   | Meaning                  |
| -------- | ------------------------ |
| `-d`     | Detached/background mode |
| `-it`    | Interactive terminal     |
| `-p`     | Port mapping             |
| `--name` | Custom container name    |
| `-f`     | Follow logs              |
| `-a`     | Show all containers      |
| `-i`     | Interactive              |
| `-t`     | Allocate terminal        |


**In short:** Docker provides a way to package, deploy, and run applications consistently using lightweight containers.
