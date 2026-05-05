# 📘 Day 25 – Real-World Multi-Container Deployment using Docker Compose (Node.js + MongoDB)

---

## 🔷 1. Conceptual Understanding

In real-world applications, services do not operate in isolation. A typical backend system includes:

* Application server
* Database
* Networking layer
* Environment configuration

Docker Compose allows you to orchestrate all these components into a **single reproducible system**.

---

### 🔹 Core Definition

> A multi-container application is a system where multiple interdependent services run in separate containers but function together as a single application.

---

## 🔷 2. Architecture Overview

We will deploy a simple system:

```text id="d25a"
Node.js Application → MongoDB Database
```

* Node.js handles API logic
* MongoDB stores data
* Both communicate via Docker network

---

## 🔷 3. Project Structure

```text id="d25b"
project/
│
├── app.js
├── package.json
├── Dockerfile
└── docker-compose.yml
```

---

## 🔷 4. Node.js Application (app.js)

```javascript id="d25c"
const express = require('express');
const mongoose = require('mongoose');

const app = express();

mongoose.connect('mongodb://mongo:27017/test');

app.get('/', (req, res) => {
  res.send("Hello from Dockerized App");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

---

## 🔷 5. Dockerfile for Node.js

```dockerfile id="d25d"
FROM node:18

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["node", "app.js"]
```

---

## 🔷 6. Docker Compose Configuration

```yaml id="d25e"
version: "3"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    ports:
      - "27017:27017"
```

---

## 🔷 7. Key Concepts Used

### 🔹 `services`

Defines multiple containers.

### 🔹 `build`

Builds image from Dockerfile.

### 🔹 `depends_on`

Ensures MongoDB starts before app.

### 🔹 `ports`

Maps container ports to host.

---

## 🔷 8. Running the Application

---

### 🔹 Step 1: Build and Start

```bash id="d25f"
docker-compose up -d
```

---

### 🔹 Step 2: Verify Running Containers

```bash id="d25g"
docker ps
```

---

### 🔹 Step 3: Access Application

```text id="d25h"
http://localhost:3000
```

---

### 🔹 Step 4: Stop Services

```bash id="d25i"
docker-compose down
```

---

## 🔷 9. Networking Behavior

Docker Compose automatically creates a network:

* Service name acts as hostname
* `mongo` is accessible from `app`

Example:

```text id="d25j"
mongodb://mongo:27017
```

---

## 🔷 10. Persistent Storage (Optional Improvement)

To persist MongoDB data:

```yaml id="d25k"
volumes:
  - mongo_data:/data/db

volumes:
  mongo_data:
```

---

## 🔷 11. Best Practices Applied

* Separate services (app + database)
* Use service names for communication
* Avoid hardcoding IP addresses
* Use `depends_on` for ordering
* Keep containers lightweight

---

## 🔷 12. Real-World Relevance

This architecture is used in:

* Web applications
* Backend APIs
* Microservices platforms

Supported by
Docker
for building scalable distributed systems.

---

## 🔷 13. Interview-Ready Definitions

**Docker Compose**
Tool for defining and managing multi-container applications.

**Service Dependency**
Defines startup order between services.

**Multi-Container Application**
Application composed of multiple interconnected containers.

---

## 🔷 14. Key Insights

* Real applications require multiple services
* Docker Compose simplifies orchestration
* Networking is automatic and efficient
* Microservices architecture improves scalability

---

## 🔷 15. Final Summary (Unit I + II Completion)

You have now mastered:

✔ Container fundamentals
✔ Docker architecture
✔ Image building and layering
✔ Storage and networking
✔ Registries and CI/CD integration
✔ Orchestration basics
✔ Multi-container deployments

This completes your **Unit I and Unit II with practical depth**.

---

