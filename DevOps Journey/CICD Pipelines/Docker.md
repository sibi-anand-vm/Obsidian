![[Pasted image 20250223083852.png]]
**What is Docker?**

Docker is a platform that allows you to develop, ship, and run applications in isolated environments called containers. Think of containers as lightweight, portable virtual machines that package your application and all its dependencies together. This ensures your application runs consistently across different environments.

**Why Docker?**

- **Consistency:** "It works on my machine" becomes a thing of the past.
- **Portability:** Containers can run on any system that supports Docker.
- **Efficiency:** Containers share the host OS kernel, making them lightweight and fast.
- **Isolation:** Applications are isolated, preventing conflicts.
- **Scalability:** Easily scale applications by running multiple containers.
- ![[Pasted image 20250223084102.png]]

### Docker Image
Docker image is like a blueprint or a template. It's a read-only file that contains instructions for creating a Docker container. Here's a more detailed breakdown:  

- **What it contains:**
    - A Docker image bundles together everything an application needs to run:
        - Code
        - Runtime environment (like a specific version of Python or Java)  
            
        - System tools  
            
        - Libraries
        - Settings
- **Read-only nature:**
    - Docker images are immutable, meaning they cannot be changed once they are created. If you need to make changes, you create a new image.  
        
- **Layers:**
    - Docker images are built in layers. Each layer represents a change to the image. This layering system makes Docker efficient, as changes can be shared between images.  
        
- **Purpose:**
    - The primary purpose of a Docker image is to provide a consistent and reliable way to package and distribute applications.  
        
    - This ensures that an application will run the same way regardless of the environment it's deployed in.  
        
- **Relationship to containers:**
    - A Docker container is a running instance of a Docker image. Think of the image as the recipe, and the container as the actual dish you cooked.
![[Pasted image 20250223110050.png]]
![[Pasted image 20250223112407.png]]

##### Software and Image
![[Pasted image 20250223110126.png]]
##### Docker File
![[Pasted image 20250223110211.png]]

##### DockerHub
![[Pasted image 20250223110320.png]]

### 🧠 1. **Docker Client (`docker`)**

- What it is: The **CLI (Command Line Interface)** tool that **you interact with**.
    
- Purpose: Sends commands to the Docker Daemon (like `docker build`, `docker run`, `docker pull`).
    
- Works via: REST API calls to the Docker Daemon.
    

📌 **Think of it as:** The **remote control** you use to manage containers.

---

### 🔧 2. **Docker Daemon (`dockerd`)**

- What it is: The **background service** that does the heavy lifting.
    
- Purpose:
    
    - Builds, runs, and manages containers.
        
    - Handles all Docker objects (images, containers, volumes, networks).
        
- Listens for requests from:
    
    - Docker Client
        
    - Docker API (direct programmatic access)
        

📌 **Think of it as:** The **engine** that powers everything.

---

### 📦 3. **Docker Registry**

- What it is: A **repository for Docker images**.
    
- Purpose:
    
    - Stores Docker images.
        
    - Allows you to **push** (upload) and **pull** (download) images.
        
- Examples:
    
    - **Docker Hub** (default public registry)
        
    - **Self-hosted** registries (for private images)
        

📌 **Think of it as:** The **app store** for Docker images.

---

### 🔁 Simple Flow:

```
You (Client)  -->  tell Docker Daemon  -->  which pulls/pushes images from/to Docker Registry
                      |
                      -->  manages containers locally

```