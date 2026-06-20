To pull out a image from docker Hub:
```
docker pull hello-world
```

Run the image file
```
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