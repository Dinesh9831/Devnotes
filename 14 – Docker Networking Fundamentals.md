# 📘 Day 14 – Docker Networking Fundamentals (Bridge, Host, and Container Communication)

---

## 🔷 1. Conceptual Understanding

When containers run on a host system, they need a way to communicate:

* With other containers
* With the host machine
* With external networks

Docker networking provides **virtual network interfaces and communication mechanisms** that allow containers to interact securely and efficiently.

---

### 🔹 Core Definition

> Docker networking is a system that enables communication between containers, between containers and the host system, and with external networks.

---

## 🔷 2. Why Networking Is Important in Containers

Containers typically run distributed applications such as:

* Web servers
* Databases
* APIs
* Microservices

These components must communicate through networks.

Example architecture:

```text id="n14a"
Browser → Web Container → API Container → Database Container
```

Without networking, containers would be isolated and unable to interact.

---

## 🔷 3. Docker Network Drivers

Docker provides several **network drivers** that define how containers communicate.

The most important ones are:

| Network Driver | Description                           |
| -------------- | ------------------------------------- |
| Bridge         | Default network for containers        |
| Host           | Container shares host network         |
| Overlay        | Used in multi-host container clusters |
| None           | No network access                     |

For basic container setups, **Bridge and Host networks** are most commonly used.

---

## 🔷 4. Bridge Network (Default Network)

The **bridge network** is the default network created by Docker.

When a container runs without specifying a network, it automatically connects to the bridge network.

---

### 🔹 Characteristics

* Containers receive their own internal IP addresses
* Containers can communicate using IP addresses
* Host-to-container communication occurs via port mapping

---

### 🔹 View Existing Networks

```bash id="n14b"
docker network ls
```

Example output:

```text id="n14c"
NETWORK ID     NAME      DRIVER
a1b2c3d4       bridge    bridge
e5f6g7h8       host      host
i9j0k1l2       none      null
```

---

### 🔹 Inspect Bridge Network

```bash id="n14d"
docker network inspect bridge
```

This command shows containers attached to the bridge network and their IP addresses.

---

## 🔷 5. Creating Custom Bridge Networks

Custom networks allow containers to communicate using **container names instead of IP addresses**.

---

### 🔹 Create Network

```bash id="n14e"
docker network create mynetwork
```

---

### 🔹 Run Containers in Network

```bash id="n14f"
docker run -d --name web --network mynetwork nginx
```

```bash id="n14g"
docker run -d --name database --network mynetwork mysql
```

Now containers can communicate using:

```text id="n14h"
web → database
```

---

## 🔷 6. Host Network

In host networking mode, the container **shares the host system's network stack**.

---

### 🔹 Characteristics

* No network isolation
* Container uses host's IP address
* Higher network performance

---

### 🔹 Example Command

```bash id="n14i"
docker run --network host nginx
```

In this case:

* nginx runs directly on host network
* No port mapping required

---

## 🔷 7. Port Mapping

Port mapping allows external systems to access container services.

---

### 🔹 Syntax

```bash id="n14j"
docker run -p host_port:container_port image_name
```

---

### 🔹 Example

```bash id="n14k"
docker run -d -p 8080:80 nginx
```

Explanation:

* Container port **80**
* Host port **8080**

Access service at:

```text id="n14l"
http://localhost:8080
```

---

## 🔷 8. Container-to-Container Communication

Containers on the same network communicate directly.

Example:

```text id="n14m"
Frontend container → Backend container → Database container
```

Communication uses:

* container name
* container IP address
* DNS resolution inside Docker network

---

## 🔷 9. DNS Resolution in Docker

Docker provides built-in **DNS services**.

This means containers can resolve each other by name.

Example:

```text id="n14n"
ping database
```

Instead of using:

```text id="n14o"
ping 172.17.0.2
```

---

## 🔷 10. Best Practices for Docker Networking

* Use **custom bridge networks** for multi-container apps
* Avoid relying on container IP addresses
* Use **container names for communication**
* Expose only necessary ports

---

## 🔷 11. Role in Container Ecosystem

Networking is fundamental for platforms like
Docker
to support scalable microservices and distributed applications.

---

## 🔷 12. Interview-Ready Definitions

**Docker Network:**
A virtual network that allows containers to communicate with each other and external systems.

**Bridge Network:**
Default Docker network providing isolated communication between containers.

**Host Network:**
Networking mode where container shares host system's network.

**Port Mapping:**
Technique to expose container services to external networks.

---

## 🔷 13. Key Insights

* Containers require networking for distributed applications.
* Bridge networks provide isolated container communication.
* Host networking removes isolation but improves performance.
* Port mapping enables external access to container services.

---

## 🔷 14. Summary

Docker networking enables containers to interact within distributed environments.

Through:

* bridge networks
* host networking
* DNS-based container discovery

Docker allows applications to be deployed as **connected microservices**.

---