# 🐳 Docker Components

## 📌 What is Docker?

Docker is a platform used to **build, ship, and run applications in containers**.

---

## 🔑 Core Docker Components

### 1. 🧠 Docker Engine

- Core part of Docker (brain)
- Runs and manages containers

Includes:
- **Docker Daemon (dockerd)** → does all work
- **REST API** → communication layer
- **Docker CLI** → user commands

👉 Responsible for:
- Creating containers
- Managing images
- Networking
- Resource allocation

---

### 2. 📦 Docker Image

- Read-only template
- Used to create containers

Contains:
- Application code
- Dependencies
- Runtime
- Libraries

👉 Built using:
docker build

---

### 3. 🚀 Docker Container

- Running instance of an image
- Lightweight and isolated

👉 Created using:
docker run

👉 Can be:
- Started
- Stopped
- Deleted

---

### 4. 📄 Dockerfile

- Text file with instructions to build image

Example:
FROM node:18  
WORKDIR /app  
COPY . .  
RUN npm install  
CMD ["node", "app.js"]

---

### 5. 📚 Docker Registry

Docker Registry is a **storage and distribution system for Docker images**.  
  
👉 It stores images so you can:  
- **Push** (upload) images  
- **Pull** (download) images  
  
---  
  
## 🔑 Types of Docker Registry  
  
### 1. 🌍 Public Registry  
  
- Available to everyone  
- Default registry used by Docker  
  
Example:  
- Docker Hub  
  
👉 Command:  
docker pull nginx  
  
---  
  
### 2. 🔒 Private Registry  
  
- Used by companies  
- Secure and restricted access  
  
Examples:  
- AWS ECR  
- Azure Container Registry  
- Self-hosted registry

---

### 6. 🌐 Docker Network

- Enables communication between containers

Types:
- bridge (default)
- host
- none

---

### 7. 💾 Docker Volume

- Used for persistent storage

👉 Data is safe even if container is deleted

---

## 🔄 Flow of Docker

1. Write Dockerfile  
2. Build Image  
3. Run Container  
4. Push/Pull from Registry  

---

## 🧠 Simple Understanding

- Docker Engine → Brain 🧠  
- Image → Blueprint 📄  
- Container → Running app 🚀  
- Dockerfile → Recipe 🧾  
- Registry → Storage 📦  

---

## 💡 Interview One-Liners

**Docker Engine:**  
"Manages containers and images."

**Image:**  
"Read-only template to create containers."

**Container:**  
"Running instance of an image."

**Dockerfile:**  
"Instructions to build an image."

**Registry:**  
"Stores and distributes images."

## 🐳 Creating Docker Images

### 🔹 1. From Dockerfile (Recommended ✅)

docker build -t myapp .

- Uses a **Dockerfile**
- Step-by-step instructions to build image
- Reproducible and clean

👉 Best practice in real-world projects

---

### 🔹 2. From Running Container

docker commit <container_id> myapp

- Creates image from a **running/stopped container**
- Captures current state

👉 Quick but not recommended for production

---

## ⚖️ Comparison

| Feature            | Dockerfile        | Container Commit     |
|-------------------|------------------|---------------------|
| Reproducible      | ✅ Yes           | ❌ No               |
| Transparency      | ✅ Clear steps   | ❌ Hidden changes   |
| Best Practice     | ✅ Industry use  | ❌ Rare use         |
| Use Case          | Development/Prod | Debugging/testing   |

---

## 🧠 Simple Understanding

- **Dockerfile** → Recipe 📄  
- **Image** → Prepared dish 🍱  
- **Container** → Running dish 🍽️  

👉 `docker commit` = saving current dish state  
👉 `docker build` = cooking using recipe

---

## 💡 When to Use What?

### Use Dockerfile when:
- Building apps
- Working in teams
- CI/CD pipelines

### Use docker commit when:
- Debugging
- Temporary backup
- Experimenting

---

## 💡 Interview One-Liner

"Images can be created using a Dockerfile (recommended) or by committing a running container, but Dockerfiles are preferred for reproducibility and maintainability."