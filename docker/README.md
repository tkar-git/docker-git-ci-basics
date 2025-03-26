# Introduction to Docker Basics

## Docker Installation
For installation of Docker, please refer to the official [Docker documentation](https://docs.docker.com/get-docker/).

## Example Docker Commands
Assuming that Docker is installed, the following commands can be used to interact with Docker:

- First open a terminal and check if Docker is installed by running `docker --version`

- Run the following commands in the terminal:
```bash
# Start docker service by running the following or open Docker Desktop
sudo systemctl start docker

# Check if Docker service is running by running
sudo systemctl status docker

# Pull a Docker image from Docker Hub by running 
docker pull hello-world

# Run the Docker image by running 
docker run hello-world

# List all running containers by running 
docker ps

# List all containers by running 
docker ps -a

# Stop a running container by running 
docker stop <container_id>

# Remove a container by running 
docker rm <container_id>

# Remove an image by running 
docker rmi <image_id>
```

## Dockerfile
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession.