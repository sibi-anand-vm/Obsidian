To see docker engine info like version plugins installed:
```
docker info
```

To pull out a image from docker Hub:
```
docker pull image-name
docker pull hello-world
```

To see all images in local machine:
```
docker images
```

Run the image file

```
docker run image-name
docker run hello-world
```
![[Pasted image 20250223112423.png]]
Every image runs,it will create an container.

To see all containers (both running and stopped), use:
```
docker ps -a
```
To see **only running** containers, use:
```
docker ps
```
Create a file named **Dockerfile** and copy paste the follow code.
![[Pasted image 20250223113858.png]]

```
FROM alpine:latest
CMD:["echo","Hello, Docker!"]
```

Go to Terminal where Dockerfile is created and run below:
```
docker build -t my-sample-image
```

Run the image:
```
docker run my-sample-image
```

Run the Container with container name or container ID:
```
 dockerFolder/ docker start lucid_williamson
lucid_williamson
 dockerFolder/ docker start 6960dad57cba
6960dad57cba
```

Lets install node image from DockerHub:
```
docker pull node
```

Lets run the node image:
```
docker run -it node
```

docker run -it node bash starts a Bash shell inside the Node image (if bash is available).

Lets start with a container ID or Name:
```
docker start NODE_ID
```
![[Pasted image 20250817040655.png]]
Execute commands:
```
docker exec -it NODE_NAME bin/bash
ls
```
![[Pasted image 20250817040954.png]]
Find NODE_PROGRAM:
```
cd usr/local/bin
ls
```
![[Pasted image 20250817041208.png]]
 Start node:
![[Pasted image 20250817041923.png]]
Stop the node container in new terminal:
```
docker stop NODE_ID
```

Tag a container and rename it:
```
//Tag a container
docker run --name container_name image_name
docker run --name node_container node

//Rename a container
docker rename old_name new_name
docker rename node_container node_container1
```
![[Pasted image 20250817043859.png]]

Delete stopped containers:
```
docker container prune
```

Delete specific container:
```
docker rm [container_name]
```

Copy a file to Container:
```
docker cp sample.txt alpine_container:/example.txt
Successfully copied 2.05kB to alpine_container:/example.txt
docker cp sample.txt alpine_container:/home/example.txt
Successfully copied 2.05kB to alpine_container:/home/example.txt
```
![[Pasted image 20250817052124.png]]

Copy a file from container:
```
docker cp alpine_container:/home/example.txt sample1.txt
Successfully copied 2.05kB to /run/media/captainjack/CaptainJack/Docker/sample1.txt
```
![[Pasted image 20250817052254.png]]

Delete a image:
```
docker rmi image_name
```

Tag a Image with repo:
```
docker tag a_sample_image:latest sibianand/samplerepo:Version1
```
![[Pasted image 20250817055606.png]]
Push a image:
```
docker push sibianand/samplerepo:Version1
```
Pull a image:
```
docker pull sibianand/samplerepo:Version1
```

You can delete in Remote Repo by using dockerHUB GUI.