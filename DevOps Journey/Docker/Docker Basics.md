## 📁 Docker Basics

### Common Commands

```bash
docker build -t myapp .
docker run -d -p 3000:3000 myapp
docker ps
docker stop <container_id>
```

## 🐳 Docker Commands Explained

### 1. 🏗️ Build Image
docker build -t myapp .

- `build` → Create a Docker image
- `-t myapp` → Tag (name) the image as **myapp**
- `.` → Current directory (contains Dockerfile)

👉 Creates an image from your project

---

### 2. ▶️ Run Container

### 📌 Command  
docker run --name mycontainer myapp  
  
---  
  
### 🔍 Meaning  
  
- `docker run` → create & start container  
- `--name mycontainer` → your custom name  
- `myapp` → image name  
  
---  
  
### ✅ Example  
docker run -d --name app1 myapp  
  
👉 Creates container named **app1**  
👉 Runs in background  
  
---  
  
### ⚠️ Without Name  
docker run myapp  
  
👉 Docker gives random name  
(e.g., funny_cat)


docker run -d -p 3000:3000 myapp

- `run` → Start a container
- `-d` → Run in background (detached mode )

 ### 🔹 Without Detached Mode  
	  docker run myapp  
  👉 Runs in **foreground**  
  👉 You see logs in terminal  
  👉 Terminal gets blocked
  
- `-p 3000:3000` → Port mapping  
  - Left (3000) → Host port  
  - Right (3000) → Container port
👉 Means:  
- Host (your laptop) → port 3000  
- Container → port 3000  
## 🔥 Why Port Mapping Needed?  
  
Containers are **isolated** 🚫  
  
👉 Without mapping:  
- App runs inside container  
- You **cannot access it from browser**  
  
---  
## 📊 Example  
  
docker run -p 8080:3000 myapp  
  
👉 Flow:  
Browser → localhost:8080 → Container:3000 → App
- `myapp` → Image name

👉 Runs your app in a container

---

### 3. 📋 List Running Containers
docker ps

- Shows all **running containers**
- Displays:
  - Container ID
  - Image name
  - Status
  - Ports

👉 Used to check active containers

---

### 4. ⛔ Stop Container
docker stop <container_id>

- Stops a running container
- `<container_id>` → ID from `docker ps`

## Cleanup

Containers can quickly clutter your hard drive if you don't delete them.

- **`docker stop [id/name]`**: Gracefully shuts down a running container.
    
- **`docker kill [id/name]`**: Forcefully stops a container (like pulling the plug).
    
- **`docker rm [id/name]`**: Deletes a **stopped** container.

- **`docker container prune`**: Deletes all containers that are currently stopped.
👉 Gracefully shuts down container

---

## 🧠 Simple Flow

1. Build → Image created  
2. Run → Container starts  
3. ps → Check running containers  
4. Stop → Stop container  

---

## 💡 One-Line Summary

"These commands build an image, run it as a container, monitor it, and stop it when needed."


## 🐳 docker run vs docker create

### 🔹 docker run

docker run myapp

👉 Creates + Starts container in one step

- Pulls image (if not present)
- Creates container
- Starts container

✅ Most commonly used

---

### 🔹 docker create

docker create myapp

👉 Only creates container (does NOT start)

- Container is in **stopped state**

👉 To start:
docker start <container_id>

---

## ⚖️ Difference

| Feature        | docker run        | docker create      |
|---------------|------------------|--------------------|
| Creates       | ✅ Yes           | ✅ Yes             |
| Starts        | ✅ Yes           | ❌ No              |
| Usage         | Daily use        | Advanced control   |

---

## 🧠 Simple Idea

- `run` → create + start 🚀  
- `create` → only create ⏸️  

---

## 💡 Example Flow

docker create --name app1 myapp  
docker start app1  

---

## 💡 One Line

"`docker run` creates and starts a container, while `docker create` only creates it without starting."