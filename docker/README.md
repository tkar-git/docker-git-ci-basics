# Introduction to Docker Basics

## Docker Installation
For installation of Docker, please refer to the official [Docker documentation](https://docs.docker.com/get-docker/).

## Example Docker Commands
Assuming that Docker is installed, the following commands can be used to interact with Docker:

- First open a terminal and check if Docker is installed by running `docker --version`

- Run the following commands in the terminal:

Start docker service by running the following or open Docker Desktop
```bash
sudo systemctl start docker
```
Check if Docker service is running by running
```bash
sudo systemctl status docker
```
Pull a Docker image from Docker Hub by running 
```bash
docker pull hello-world
```
Run the Docker image by running 
```bash
docker run hello-world
```
List all running containers by running 
```bash
docker ps
```
List all containers by running 
```bash
docker ps -a
```
Stop a running container by running 
```bash
docker stop <container_id>
```
Remove a container by running 
```bash
docker rm <container_id>
```
Remove an image by running
```bash 
docker rmi <image_id>
```

## Dockerfile
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession.

Below is an example of a Dockerfile:
```Dockerfile
# Start with a basic Ubuntu image
FROM ubuntu:latest

# Prevent interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install Python and Git
RUN apt-get update && apt-get install -y python3 git

# Set the default command to run when the container starts
CMD ["bash"]
```
Copy the above code into a file named `Dockerfile` and run the following command in the same directory as the Dockerfile:
```bash
docker build -t minimalist_linux .
```
You will see an output similar to the following:
```output
[+] Building 50.2s (6/6) FINISHED                                                                                                                  docker:desktop-linux
 => [internal] load build definition from dockerfile                                                                                                               0.1s
 => => transferring dockerfile: 362B                                                                                                                               0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                                   1.6s
 => [internal] load .dockerignore                                                                                                                                  0.1s
 => => transferring context: 2B                                                                                                                                    0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest@sha256:72297848456d5d37d1262630108ab308d3e9ec7ed1c3286a32fe09856619a782                                             1.8s
 => => resolve docker.io/library/ubuntu:latest@sha256:72297848456d5d37d1262630108ab308d3e9ec7ed1c3286a32fe09856619a782                                             0.0s
 => => sha256:5a7813e071bfadf18aaa6ca8318be4824a9b6297b3240f2cc84c1db6f4113040 29.75MB / 29.75MB                                                                   1.0s
 => => extracting sha256:5a7813e071bfadf18aaa6ca8318be4824a9b6297b3240f2cc84c1db6f4113040                                                                          0.6s
 => [2/2] RUN apt-get update && apt-get install -y python3 git                                                                                                    39.4s
 => exporting to image                                                                                                                                             7.0s 
 => => exporting layers                                                                                                                                            5.4s 
 => => exporting manifest sha256:627fcc9bf8742b4de7493a281e36d54918de2e910f10e1b55b27af396de9bdd7                                                                  0.1s 
 => => exporting config sha256:dabe55fef6b4051f8b753df79cab22c28a39056f3566b2ec26b87587afe2e3ff                                                                    0.1s 
 => => exporting attestation manifest sha256:ea06d99c7c5041a76e5dbf91897483c95a431fdbf7a8597818a63916a4ea145d                                                      0.1s 
 => => exporting manifest list sha256:23084ea2105291ad211b8b410ce61271abf72005c5d098e95d5c2a8ed3765a8c                                                             0.1s 
 => => naming to docker.io/library/minimalist_linux:latest                                                                                                         0.0s
 => => unpacking to docker.io/library/minimalist_linux:latest                                                                                                      1.2s

View build details: docker-desktop://dashboard/build/...
```
You have now successfully built your first Docker image. You can list all images by running:
```bash
docker images
```

You can run the image by running:
```bash
docker run -it minimalist_linux
```
Here `-it` is used to run the container in interactive mode. Additionally, you can add the `--rm` flag to remove the container when it exits.