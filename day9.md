# 📘 Day 9 – Docker CLI & Docker Object Management

---

## 🔷 1. Conceptual Understanding

Docker CLI is the **primary interface** for interacting with Docker Daemon. All container operations—build, run, inspect, stop—are executed via CLI commands.

---

### 🔹 Core Definition

> Docker CLI (Command Line Interface) is the tool through which users communicate with Docker daemon to manage containers, images, networks, and volumes.

---

## 🔷 2. Docker Objects Overview

Docker manages four main object types:

1. **Containers** – running instances of images
2. **Images** – read-only templates for containers
3. **Volumes** – persistent storage
4. **Networks** – communication between containers

---

### 🔹 Key Insight

Containers cannot exist without images.
Volumes and networks enhance container functionality.

---

## 🔷 3. Containers – Life Cycle Management

---

### 🔹 Run a Container

```bash id="c9r1"
docker run -d --name webserver nginx
```

* `-d` → detached mode
* `--name` → assign container name
* `nginx` → image name

---

### 🔹 List Running Containers

```bash id="c9r2"
docker ps
```

---

### 🔹 List All Containers

```bash id="c9r3"
docker ps -a
```

---

### 🔹 Stop a Container

```bash id="c9r4"
docker stop webserver
```

---

### 🔹 Remove a Container

```bash id="c9r5"
docker rm webserver
```

---

## 🔷 4. Images – Build, Pull, Tag, Remove

---

### 🔹 Pull an Image from Registry

```bash id="i9p1"
docker pull ubuntu:22.04
```

---

### 🔹 Build an Image from Dockerfile

```bash id="i9p2"
docker build -t myapp:1.0 .
```

* `-t` → tag image
* `.` → current build context

---

### 🔹 List Images

```bash id="i9p3"
docker images
```

---

### 🔹 Remove an Image

```bash id="i9p4"
docker rmi myapp:1.0
```

---

### 🔹 Inspect Image Layers

```bash id="i9p5"
docker history myapp:1.0
```

---

## 🔷 5. Volumes – Persistent Storage

---

### 🔹 Create a Volume

```bash id="v9p1"
docker volume create appdata
```

---

### 🔹 Attach Volume to Container

```bash id="v9p2"
docker run -d -v appdata:/data --name mycontainer ubuntu
```

* Maps host volume `appdata` to container `/data`

---

### 🔹 List Volumes

```bash id="v9p3"
docker volume ls
```

---

### 🔹 Remove Volume

```bash id="v9p4"
docker volume rm appdata
```

---

## 🔷 6. Networks – Container Communication

---

### 🔹 List Networks

```bash id="n9p1"
docker network ls
```

---

### 🔹 Create a Network

```bash id="n9p2"
docker network create mynet
```

---

### 🔹 Connect Container to Network

```bash id="n9p3"
docker run -d --name app1 --network mynet nginx
```

---

### 🔹 Inspect Network

```bash id="n9p4"
docker network inspect mynet
```

---

## 🔷 7. Practical Tips & Best Practices

1. Always **name containers** to simplify management
2. Remove unused containers and images to save space (`docker system prune`)
3. Use volumes for persistent data, not container writable layer
4. Use bridge networks for multi-container applications
5. Tag images properly before pushing to registries

---

## 🔷 8. Real-World Analogy

Think of Docker objects like:

* **Images:** Blueprints
* **Containers:** Houses built from blueprints
* **Volumes:** Storage rooms
* **Networks:** Roads connecting houses

---

## 🔷 9. Interview-Ready Definitions

**Docker CLI:**
Command line tool to manage Docker daemon and objects.

**Container:**
A running instance of a Docker image with its own filesystem, network, and process space.

**Image:**
Read-only template used to create containers.

**Volume:**
Persistent storage that survives container lifecycle.

**Network:**
Virtual layer allowing communication between containers.

---

## 🔷 10. Key Insights (You Must Internalize)

* CLI mastery = daily DevOps productivity
* Containers = ephemeral, Volumes = persistent
* Networks enable scalable multi-container apps
* Understanding object relationships is critical for Docker Compose and CI/CD

---

## 🔷 11. Summary

Docker CLI is your **primary tool**.
Mastering containers, images, networks, and volumes prepares you for:

* Dockerfile creation
* Multi-container applications (Docker Compose)
* Continuous Integration pipelines

---

## 🔷 12. What Comes Next

Next, you will study:

➡ **Dockerfile Core Concepts & Image Building** (Unit II)

This is the point where **Docker CLI knowledge meets image creation and optimization**.

---
