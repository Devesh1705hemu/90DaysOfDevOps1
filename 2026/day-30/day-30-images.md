# 🚀 Day 30: Docker Images, Layers & Container Lifecycle

As part of the **#90DaysOfDevOps** challenge by **TrainWithShubham**, I practiced Docker images, image layers, container lifecycle management, running containers, and Docker cleanup.

---

## 📌 Task 1: Docker Images

### 1. Pull Docker Images

Pull the `nginx`, `ubuntu`, and `alpine` images from Docker Hub.

```bash
docker pull nginx
docker pull ubuntu
docker pull alpine
```

### 2. List Docker Images

To list all images available on the local machine:

```bash
docker images
```

Or:

```bash
docker image ls
```

Example:

```text
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    xxxxxxxx       ...            ...
ubuntu       latest    xxxxxxxx       ...            ...
alpine       latest    xxxxxxxx       ...            ...
```

### 3. Ubuntu vs Alpine

Compare the sizes of the `ubuntu` and `alpine` images:

```bash
docker images ubuntu alpine
```

#### Why is Alpine much smaller?

**Alpine Linux** is designed to be extremely lightweight. It contains only the essential components required to run applications.

Ubuntu is a more complete general-purpose Linux distribution and includes many additional packages and utilities.

| Image  | General Characteristics                    |
| ------ | ------------------------------------------ |
| Ubuntu | Full-featured Linux distribution           |
| Alpine | Minimal and lightweight Linux distribution |

The smaller Alpine image can help reduce:

* Image download time
* Storage usage
* Container startup overhead
* Network transfer
* Container attack surface

> **Note:** Smaller does not automatically mean better. The right base image depends on the application's requirements and compatibility.

### 4. Inspect an Image

Use `docker image inspect` to view detailed information about an image:

```bash
docker image inspect nginx
```

You can find information such as:

* Image ID
* Created date
* Architecture
* Operating system
* Environment variables
* Entrypoint
* Default command
* Exposed ports
* Root filesystem
* Image layers
* Metadata

### 5. Remove an Image

To remove an image that is no longer required:

```bash
docker rmi alpine
```

Alternative:

```bash
docker image rm alpine
```

If the image is being used by a container, remove the container first or use the appropriate cleanup command.

---

# 📦 Task 2: Image Layers

## 1. View Image History

Run:

```bash
docker image history nginx
```

This shows the history of how the Docker image was built.

Example:

```text
IMAGE        CREATED       CREATED BY                         SIZE
xxxxxxxx     ...           /bin/sh -c ...                     ...
xxxxxxxx     ...           /bin/sh -c ...                     ...
xxxxxxxx     ...           ENTRYPOINT ["..."]                  0B
```

## 2. Understanding Layers

Each filesystem-changing instruction in a Docker image can contribute a **layer**.

Some entries may show a size such as:

```text
25MB
10MB
5MB
```

Others may show:

```text
0B
```

A `0B` entry often represents metadata or configuration changes that do not add filesystem content.

## 3. What Are Docker Image Layers?

Docker images are built using multiple layers.

For example, a Dockerfile might contain:

```dockerfile
FROM ubuntu

RUN apt-get update

RUN apt-get install -y nginx

COPY index.html /var/www/html/
```

Each filesystem-changing instruction can create another layer.

### Why does Docker use layers?

Docker uses layers because they provide:

* **Reusability**: Multiple images can share the same layers.
* **Caching**: Docker can reuse unchanged layers during builds.
* **Efficiency**: Only changed layers need to be rebuilt or transferred.
* **Storage optimization**: Shared layers do not need to be stored multiple times.

### Important Concept

Docker images are generally **read-only**, while containers add a writable layer on top of the image.

```text
Container Writable Layer
          ↓
Image Layer
Image Layer
Image Layer
Base Layer
```

---

# 🔄 Task 3: Container Lifecycle

For this task, use an Nginx container.

## 1. Create a Container Without Starting It

```bash
docker create --name lifecycle-demo nginx
```

Check the container:

```bash
docker ps -a
```

The container should have a `Created` status.

---

## 2. Start the Container

```bash
docker start lifecycle-demo
```

Check:

```bash
docker ps -a
```

The container should now be running.

---

## 3. Pause the Container

```bash
docker pause lifecycle-demo
```

Check status:

```bash
docker ps -a
```

You can also check:

```bash
docker inspect -f '{{.State.Status}}' lifecycle-demo
```

---

## 4. Unpause the Container

```bash
docker unpause lifecycle-demo
```

Check:

```bash
docker ps
```

---

## 5. Stop the Container

```bash
docker stop lifecycle-demo
```

Check:

```bash
docker ps -a
```

The container should show an exited/stopped state.

---

## 6. Restart the Container

```bash
docker restart lifecycle-demo
```

Check:

```bash
docker ps
```

---

## 7. Kill the Container

```bash
docker kill lifecycle-demo
```

Check:

```bash
docker ps -a
```

### `stop` vs `kill`

| Command       | Purpose                              |
| ------------- | ------------------------------------ |
| `docker stop` | Gracefully stops the container       |
| `docker kill` | Immediately terminates the container |

---

## 8. Remove the Container

If the container is still running, stop it first:

```bash
docker stop lifecycle-demo
```

Then remove it:

```bash
docker rm lifecycle-demo
```

Verify:

```bash
docker ps -a
```

---

# 🐳 Task 4: Working with Running Containers

## 1. Run an Nginx Container in Detached Mode

```bash
docker run -d --name nginx-demo -p 8080:80 nginx
```

Check the running container:

```bash
docker ps
```

Open in your browser:

```text
http://localhost:8080
```

You should see the Nginx welcome page.

---

## 2. View Container Logs

```bash
docker logs nginx-demo
```

---

## 3. View Real-Time Logs

Use the `-f` option to follow the logs:

```bash
docker logs -f nginx-demo
```

Press:

```text
Ctrl + C
```

to stop following the logs.

---

## 4. Exec Into the Container

Open a shell inside the running Nginx container:

```bash
docker exec -it nginx-demo /bin/bash
```

If Bash is not available:

```bash
docker exec -it nginx-demo /bin/sh
```

Explore the filesystem:

```bash
pwd
ls
ls -la
cd /etc
ls
cd /usr/share/nginx/html
ls
```

Exit the container:

```bash
exit
```

---

## 5. Run a Single Command Inside the Container

You don't always need to enter the container.

For example:

```bash
docker exec nginx-demo ls /usr/share/nginx/html
```

Check the Nginx version:

```bash
docker exec nginx-demo nginx -v
```

---

## 6. Inspect the Container

Run:

```bash
docker inspect nginx-demo
```

This provides detailed information about the container.

### Find the IP Address

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nginx-demo
```

### Find Port Mappings

```bash
docker port nginx-demo
```

Example:

```text
80/tcp -> 0.0.0.0:8080
```

### Find Mounts

```bash
docker inspect -f '{{json .Mounts}}' nginx-demo
```

The complete `docker inspect` output can also be searched for:

* IP address
* Port mappings
* Mounts
* Network configuration
* Environment variables
* Container state
* Restart policy
* Image information

---

# 🧹 Task 5: Cleanup

## 1. Stop All Running Containers

List running containers:

```bash
docker ps
```

Stop all running containers:

```bash
docker stop $(docker ps -q)
```

### Explanation

```text
docker ps -q
```

returns only the IDs of running containers.

Those IDs are then passed to:

```text
docker stop
```

---

## 2. Remove All Stopped Containers

```bash
docker container prune
```

Docker will ask for confirmation.

To skip the confirmation:

```bash
docker container prune -f
```

---

## 3. Remove Unused Images

To remove dangling images:

```bash
docker image prune
```

To remove all unused images:

```bash
docker image prune -a
```

Without confirmation:

```bash
docker image prune -a -f
```

> ⚠️ Be careful with `-a`. It can remove images that are not currently associated with containers but may still be useful later.

---

## 4. Check Docker Disk Usage

Run:

```bash
docker system df
```

This shows Docker's disk usage for:

* Images
* Containers
* Local volumes
* Build cache

For detailed information:

```bash
docker system df -v
```

---

# 🧠 Key Learnings

After completing these tasks, I practiced:

* Docker image management
* Pulling images from Docker Hub
* Listing and inspecting images
* Understanding Ubuntu vs Alpine
* Docker image layers
* Image caching and reuse
* Complete container lifecycle
* Creating containers
* Starting and stopping containers
* Pausing and unpausing containers
* Restarting and killing containers
* Removing containers
* Running containers in detached mode
* Container logs
* Real-time log monitoring
* `docker exec`
* Container filesystem exploration
* Container inspection
* IP address and port mapping
* Docker cleanup
* Docker disk usage management

---

# 📋 Important Docker Commands

| Command                      | Purpose                              |
| ---------------------------- | ------------------------------------ |
| `docker pull IMAGE`          | Download an image                    |
| `docker images`              | List images                          |
| `docker image ls`            | List images                          |
| `docker image inspect IMAGE` | Inspect an image                     |
| `docker image history IMAGE` | View image layers/history            |
| `docker rmi IMAGE`           | Remove an image                      |
| `docker create`              | Create a container                   |
| `docker run`                 | Create and start a container         |
| `docker start`               | Start a container                    |
| `docker pause`               | Pause a container                    |
| `docker unpause`             | Resume a paused container            |
| `docker stop`                | Gracefully stop a container          |
| `docker restart`             | Restart a container                  |
| `docker kill`                | Forcefully stop a container          |
| `docker rm`                  | Remove a container                   |
| `docker ps`                  | List running containers              |
| `docker ps -a`               | List all containers                  |
| `docker logs`                | View container logs                  |
| `docker exec`                | Execute a command inside a container |
| `docker inspect`             | View detailed information            |
| `docker port`                | View port mappings                   |
| `docker container prune`     | Remove stopped containers            |
| `docker image prune`         | Remove unused images                 |
| `docker system df`           | Check Docker disk usage              |

---

# 🎯 Final Takeaway

Docker is not just about running containers. Understanding **images, layers, container states, networking information, logs, inspection, and cleanup** is essential for working effectively with Docker in a DevOps environment.

> **Practice → Understand → Automate → Deploy**

## #90DaysOfDevOps

**Day 30 completed ✅**

Learning Docker one concept at a time and building stronger DevOps fundamentals.
