# 📘 Day 12 – ENTRYPOINT vs CMD and Container Startup Behavior

---

## 🔷 1. Conceptual Understanding

When a container starts, it must run a **main process**. Dockerfiles define this startup behavior using two instructions:

* **CMD**
* **ENTRYPOINT**

Both instructions determine what command runs when a container is started.

---

### 🔹 Core Definition

**CMD**

> Specifies the default command that will run when a container starts.

**ENTRYPOINT**

> Defines the main executable that always runs when the container starts.

---

## 🔷 2. CMD Instruction (Detailed)

CMD provides **default arguments or commands** that can be overridden when running the container.

---

### 🔹 Syntax

```dockerfile
CMD ["executable","param1","param2"]
```

---

### 🔹 Example

```dockerfile
FROM ubuntu
CMD ["echo","Hello Docker"]
```

When the container starts, it prints:

```
Hello Docker
```

---

### 🔹 Overriding CMD

If you run:

```bash
docker run image_name echo "New Message"
```

Output becomes:

```
New Message
```

👉 CMD can be overridden at runtime.

---

## 🔷 3. ENTRYPOINT Instruction

ENTRYPOINT defines the **main command that always runs** inside the container.

Unlike CMD, it **cannot easily be overridden**.

---

### 🔹 Syntax

```dockerfile
ENTRYPOINT ["executable","param1","param2"]
```

---

### 🔹 Example

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo","Hello from container"]
```

When container starts, it always runs that command.

---

## 🔷 4. Combining ENTRYPOINT and CMD

Best practice is often to use **ENTRYPOINT for the main executable** and **CMD for default arguments**.

---

### 🔹 Example

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello Docker"]
```

Running container normally:

```bash
docker run myimage
```

Output:

```
Hello Docker
```

Running with custom argument:

```bash
docker run myimage "DevOps"
```

Output:

```
DevOps
```

---

## 🔷 5. Exec Form vs Shell Form

Docker supports two formats for commands.

---

### 🔹 Exec Form (Recommended)

```dockerfile
CMD ["node","app.js"]
```

Advantages:

* No shell processing
* Better signal handling
* Preferred in production

---

### 🔹 Shell Form

```dockerfile
CMD node app.js
```

Runs inside shell (`/bin/sh -c`).

Disadvantages:

* Harder signal handling
* Less predictable

---

## 🔷 6. Container Startup Lifecycle

When a container starts:

1. Docker creates writable container layer
2. Networking and volumes are attached
3. ENTRYPOINT is executed
4. CMD arguments are passed
5. Application process begins running

---

### 🔹 Key Insight

The container stops when the **main process exits**.

Containers are therefore designed to run **one main process**.

---

## 🔷 7. Practical Dockerfile Example

```dockerfile
FROM python:3.10

WORKDIR /app

COPY . .

ENTRYPOINT ["python"]

CMD ["app.py"]
```

---

### Build Image

```bash
docker build -t pythonapp .
```

---

### Run Container

```bash
docker run pythonapp
```

---

### Run with Custom Script

```bash
docker run pythonapp test.py
```

---

## 🔷 8. Real-World Use Cases

ENTRYPOINT is commonly used for:

* CLI tools
* Web servers
* Database services

Example containers:

* nginx
* redis
* mysql

These containers start a **single service automatically**.

---

## 🔷 9. Common Mistakes

❌ Using multiple CMD instructions
❌ Using shell form unnecessarily
❌ Confusing ENTRYPOINT with CMD
❌ Running multiple background processes in one container

---

## 🔷 10. Interview-Ready Definitions

**CMD**
Defines default command executed when container starts and can be overridden.

**ENTRYPOINT**
Defines the primary command executed when the container starts.

**Exec Form**
Command format using JSON array syntax for better signal handling.

---

## 🔷 11. Best Practices

* Use **ENTRYPOINT for main executable**
* Use **CMD for default parameters**
* Prefer **exec form** syntax
* Design containers around **single main process**

---

## 🔷 12. Role in Container Platforms

Platforms like
Docker
rely on CMD and ENTRYPOINT to control how containerized applications start and behave during runtime.

---

## 🔷 13. Key Insights

* CMD defines default behavior
* ENTRYPOINT defines fixed behavior
* Both work together to control container startup
* Understanding startup behavior is critical for microservices deployment

---

## 🔷 14. Summary

CMD and ENTRYPOINT control **how containers execute applications**.

Correct usage ensures:

* predictable container behavior
* flexible runtime configuration
* reliable production deployments

---

