# 🐳 Containerization Notes

## 📌 What is Containerization?

Containerization is a lightweight virtualization method where applications run in **isolated environments (containers)** while sharing the host OS kernel.

> 💡 “Build once, run anywhere”

---

## 🧠 Basic Architecture

### Without Containers
Application → OS → Hardware

### With Containers
Application → Container → Container Engine → Host OS → Hardware

---

## 🔑 Key Components

### 1. Container
- Lightweight, isolated environment
- Contains:
  - Application
  - Dependencies
  - Libraries

---

### 2. Container Engine

The tool you are looking for is the **Docker Engine**.

It is the core software that acts as the "brain" for your containers. Specifically, it is the **Docker Daemon** (`dockerd`) within the engine that handles the heavy lifting you mentioned.

---

## How it handles each task:

- **Creation:** When you run `docker build` or `docker pull`, the engine prepares a read-only **Image**. When you execute `docker run`, it creates a writable layer on top of that image to form a **Container**.
    
- **Management:** The engine tracks the lifecycle of every container. It allows you to start, stop, pause, restart, and delete them, ensuring they have the resources (CPU, Memory) they need.
    
- **Networking:** The engine automatically creates a virtual bridge (usually named `docker0`) and assigns a unique private IP address to every container so they can talk to each other and the outside world.
    
- **Execution:** It uses a low-level "runtime" (typically `runc`) to talk to the Linux kernel. It sets up **Namespaces** (for isolation) and **Control Groups** (for resource limits) to ensure the container's process runs in its own "bubble."

**Examples:**
- Docker
- containerd
- CRI-O

---

### 3. Image
- Blueprint of a container
- Read-only template

Contains:
- App code
- Runtime
- Dependencies

---

## 📦 Container vs VM

| Feature   | VM          | Container        |
| --------- | ----------- | ---------------- |
| OS        | Full OS     | Shared OS kernel |
| Size      | Large (GBs) | Small (MBs)      |
| Boot Time | Slow        | Fast             |
| Isolation | Strong      | Moderate         |
|           |             |                  |


---

## 🔄 Container Lifecycle

1. Build Image
2. Run Container
3. Stop Container
4. Remove Container

---

