# Day 31 – Dockerfile: Build Your Own Images

## Task 1: Your First Dockerfile

### Dockerfile

FROM ubuntu
RUN apt-get update && apt-get install -y curl
CMD ["echo", "Hello from my custom image!"]

### Build

docker build -t my-ubuntu:v1 .

### Run

docker run --name my-first-container my-ubuntu:v1

### Output

Hello from my custom image!

---

## Task 2: Dockerfile Instructions

### Dockerfile

FROM ubuntu
RUN apt-get update && apt-get install -y python3
WORKDIR /app
COPY index.html .
EXPOSE 8000
CMD ["python3", "-m", "http.server", "8000"]

### Build

docker build -t docker-task2:v1 .

### Run

docker run -d -p 8000:8000 --name docker-task2-container docker-task2:v1

### Instructions

FROM → Base image  
RUN → Executes commands during build  
COPY → Copies files from host to image  
WORKDIR → Sets working directory  
EXPOSE → Documents the port  
CMD → Default command

---

## Task 3: CMD vs ENTRYPOINT

### CMD Dockerfile

FROM ubuntu
CMD ["echo", "hello"]

### Build

docker build -t cmd-test:v1 .

### Run

docker run --rm cmd-test:v1

### Output

hello

### Custom Command

docker run --rm cmd-test:v1 echo "custom command"

### Output

custom command

### Answer

A custom command replaces CMD.

### ENTRYPOINT Dockerfile

FROM ubuntu
ENTRYPOINT ["echo"]

### Build

docker build -t entrypoint-test:v1 .

### Run

docker run --rm entrypoint-test:v1 hello

### Output

hello

### Additional Arguments

docker run --rm entrypoint-test:v1 Hello from Docker

### Output

Hello from Docker

### Answer

Additional arguments are passed to ENTRYPOINT.

### CMD vs ENTRYPOINT

CMD → Default command that can be overridden.  
ENTRYPOINT → Main executable that normally remains fixed and accepts arguments.

---

## Task 4: Build a Simple Web App Image

### index.html

<!DOCTYPE html>
<html>
<head>
    <title>My Docker Website</title>
</head>
<body>
    <h1>Hello from my Docker Web App!</h1>
    <p>Day 31 - Dockerfile</p>
</body>
</html>

### Dockerfile

FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html

### Build

docker build -t my-website:v1 .

### Run

docker run -d -p 8080:80 --name my-website-container my-website:v1

### Open in Browser

http://localhost:8080

---

## Task 5: .dockerignore

### .dockerignore

node_modules
.git
*.md
.env

### Dockerfile

FROM nginx:alpine
COPY . /usr/share/nginx/html

### Build

docker build -t dockerignore-test:v1 .

### Run

docker run -d -p 8080:80 --name dockerignore-test-container dockerignore-test:v1

### Verify

docker exec -it dockerignore-test-container ls -la /usr/share/nginx/html

### Ignored Files

node_modules  
.git  
*.md  
.env

These files are not included in the Docker build context.

---

## Task 6: Build Optimization

### Dockerfile

FROM ubuntu
RUN apt-get update && apt-get install -y curl
WORKDIR /app
COPY app.txt .
CMD ["cat", "app.txt"]

### First Build

docker build -t optimization:v1 .

Change one line in app.txt and rebuild:

docker build -t optimization:v2 .

### Answer

Docker reuses cached layers when possible.

### Layer Order

Stable instructions should come first and frequently changing instructions should come last.

FROM → RUN → WORKDIR → COPY → CMD

### Why does layer order matter?

Docker caches each layer. When a layer changes, that layer and the following layers may need to be rebuilt. Keeping frequently changing instructions last allows Docker to reuse more cached layers and makes builds faster.
