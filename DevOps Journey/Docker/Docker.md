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
        
- **Purpose:**
    - The primary purpose of a Docker image is to provide a consistent and reliable way to package and distribute applications.  
        
    - This ensures that an application will run the same way regardless of the environment it's deployed in.  

![[Pasted image 20250223110050.png]]
![[Pasted image 20250223112407.png]]

##### Docker File
![[Pasted image 20250223110211.png]]

# Docker Image vs. Container

## The core difference

- A Docker image is a read-only blueprint (template) that includes the application, its dependencies, and configuration needed to run. It’s built from a Dockerfile and stored in registries or locally for reuse.
    
- A Docker container is a running (or stopped) instance created from an image. It adds a writable layer at runtime for state and changes and executes the process defined by the image.
    
## How they relate

- Images are used to create containers; many containers can run from the same image, each with its own isolated runtime state.
    
- Images can exist without containers; containers cannot exist without an image.

- The analogy is mostly right: think of a Docker **image** like an APK/installer package, and a Docker **container** like the installed app running on a device.

- Lifecycles:
    
    - Image: build, tag, push/pull, store, version.
        
    - Container: create, start, stop, restart, pause, remove.
## Common commands (quick mental map)

- Images: docker build, docker images, docker pull, docker push, docker rmi
    
- Containers: docker run, docker ps, docker stop, docker start, docker exec, docker rm, docker logs
## Typical workflow

1. Write a Dockerfile to define the environment.
    
2. Build an image from the Dockerfile.(When you run the command `docker build`, you are instructing the **Docker CLI** to send your **Dockerfile** and the "context" (your project files) to the **Docker Daemon**. The Daemon then uses the Builder to execute the instructions.)
    
3. Run one or more containers from that image.
    
4. If runtime changes are desired permanently, bake them into a new image via updated Dockerfile (or in a pinch, commit a container to an image).
##### DockerHub
![[Pasted image 20250223110320.png]]
Docker Hub is to container images what GitHub is to source code, but they serve different layers of the workflow. Docker Hub is a container registry for storing and distributing Docker/OCI images.