# 📘 Day 15 – Docker Storage: Volumes, Bind Mounts, and Persistent Data

---

## 🔷 1. Conceptual Understanding

Containers are designed to be **stateless and ephemeral**, meaning that when a container is removed, all data inside it is lost. However, many real-world applications require persistent storage.

Examples include:

* Databases (MySQL, PostgreSQL)
* Application logs
* Uploaded files
* Configuration data

Docker provides **storage mechanisms** that allow data to persist beyond the lifecycle of a container.

---

### 🔹 Core Definition

> Docker storage refers to mechanisms that allow containers to store and manage persistent data outside the container filesystem.

---

## 🔷 2. Why Persistent Storage Is Important

Without persistent storage:

* Data disappears when container stops
* Databases lose records
* Application files are deleted
* Logs cannot be preserved

Persistent storage ensures:

* Data durability
* Application reliability
* Easy backup and recovery

---

## 🔷 3. Types of Docker Storage

Docker mainly supports two types of persistent storage:

| Storage Type | Description                        |
| ------------ | ---------------------------------- |
| Volume       | Managed by Docker                  |
| Bind Mount   | Linked directly to host filesystem |

Both approaches allow data to persist even if the container is removed.

---

## 🔷 4. Docker Volumes

Volumes are the **recommended method** for storing persistent data.

---

### 🔹 Definition

> A Docker volume is a managed storage location on the host system used to persist container data.

---

### 🔹 Advantages

* Managed by Docker
* Easy to share between containers
* Isolated from host filesystem
* Safe and portable

---

### 🔹 Create a Volume

```bash id="s15a"
docker volume create myvolume
```

---

### 🔹 List Volumes

```bash id="s15b"
docker volume ls
```

Example output:

```text id="s15c"
DRIVER    VOLUME NAME
local     myvolume
```

---

### 🔹 Use Volume in Container

```bash id="s15d"
docker run -d -v myvolume:/app/data nginx
```

This mounts the volume to `/app/data` inside the container.

---

### 🔹 Inspect Volume

```bash id="s15e"
docker volume inspect myvolume
```

This shows the volume location on the host system.

---

## 🔷 5. Bind Mounts

Bind mounts directly connect a **host directory** to a container directory.

---

### 🔹 Definition

> A bind mount maps a directory or file from the host machine directly into the container.

---

### 🔹 Example Command

```bash id="s15f"
docker run -d -v C:\data:/app/data nginx
```

Explanation:

* `C:\data` → directory on host system
* `/app/data` → directory inside container

---

### 🔹 Advantages

* Direct access to host files
* Useful during development
* Real-time file updates

---

### 🔹 Disadvantages

* Less portable
* Depends on host filesystem structure
* Potential security risks

---

## 🔷 6. Volumes vs Bind Mounts

| Feature           | Volume     | Bind Mount      |
| ----------------- | ---------- | --------------- |
| Managed by Docker | Yes        | No              |
| Portability       | High       | Low             |
| Performance       | Good       | Depends on host |
| Use Case          | Production | Development     |

---

## 🔷 7. Sharing Data Between Containers

Volumes can be shared between multiple containers.

Example:

```bash id="s15g"
docker run -d -v shared_data:/data nginx
```

```bash id="s15h"
docker run -d -v shared_data:/data ubuntu
```

Both containers access the same storage.

---

## 🔷 8. Removing Volumes

Unused volumes can be removed to free storage.

---

### 🔹 Remove Specific Volume

```bash id="s15i"
docker volume rm myvolume
```

---

### 🔹 Remove All Unused Volumes

```bash id="s15j"
docker volume prune
```

---

## 🔷 9. Copy-on-Write Mechanism

Docker uses **Copy-on-Write (CoW)** for container storage.

---

### 🔹 How It Works

1. Base image layers are read-only
2. Container adds a writable layer
3. Changes are stored in this layer
4. Original image remains unchanged

---

### 🔹 Key Insight

This mechanism improves:

* Storage efficiency
* Container performance
* Image reusability

---

## 🔷 10. Real-World Example

Database containers require persistent storage.

Example MySQL container:

```bash id="s15k"
docker run -d -v mysql_data:/var/lib/mysql mysql
```

Here:

* Database files persist
* Even if container stops or is recreated

---

## 🔷 11. Role in Container Platforms

Storage mechanisms are essential for applications running on
Docker
because they enable stateful services such as databases and logging systems.

---

## 🔷 12. Interview-Ready Definitions

**Docker Volume:**
A Docker-managed persistent storage mechanism used to store container data.

**Bind Mount:**
A direct mapping between a host directory and container directory.

**Persistent Storage:**
Storage that retains data even after container deletion.

**Copy-on-Write:**
A mechanism where container changes are stored in a separate writable layer.

---

## 🔷 13. Key Insights

* Containers are ephemeral by design
* Persistent storage is required for real applications
* Volumes are recommended for production environments
* Bind mounts are useful for development workflows

---

## 🔷 14. Summary

Docker storage enables containers to manage persistent data through volumes and bind mounts.

These mechanisms allow applications to:

* maintain state
* preserve data
* support reliable deployments

---

