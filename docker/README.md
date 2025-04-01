# Introduction to Docker Basics

## Docker Installation
For installation of Docker, please refer to [pre-requisites](../prereq_install.md) or to the official [Docker documentation](https://docs.docker.com/get-docker/).

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
<details>

<summary style="font-size: 1.1em; color: lightcoral;">Click to view a few useful monitoring commands</summary>


</br>List all running containers by running 
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
Remove all containers by running 
```bash
docker system prune
```
Remove an image by running
```bash 
docker rmi <image_id>
```

</details>

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
docker build -t minimalist_linux:test_tag .
```
Use the -f flag to specify the Dockerfile if it is not named `Dockerfile` or is not in the current directory. The `-t` flag is used to tag the image with a name and optionally a version. 
You will see an output similar to the following: 
<details>

<summary
style="font-size: 1.1em; color: lightcoral;"> Click to view output
</summary>

```output
[+] Building 50.2s (6/6) FINISHED                                                                                                                  docker:desktop-linux
 => [internal] load build definition from dockerfile                                                                                                               0.1s
 => => transferring dockerfile: 362B                                                                                                                               0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                                   1.6s

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
</details>

</br>
You have now successfully built your first Docker image. You can list all images by running:
```bash
docker images
```

You can run the image by running:
```bash
docker run -it minimalist_linux
```
Here `-it` is used to run the container in interactive mode. Additionally, you can add the `--rm` flag to remove the container when it exits.



### Additional Features
You can add additional features to your Dockerfile. For example, if you want to install a specific version of Python, you can modify the `RUN` command in the Dockerfile. Select the version you want from the [Python release page](https://www.python.org/downloads/source/) and replace `3.12.9` with the desired version. For example, to install Python 3.8.10, you can modify the `RUN` command as follows:

```Dockerfile
RUN apt-get update && apt-get install -y python3=3.12.9 
```
To set up a working directory inside the container, you can add the following line to the Dockerfile:
```Dockerfile
WORKDIR /home/<USER>/workdir/
```
You can also add a `COPY` command to copy files from your local machine to the Docker image:
```Dockerfile
COPY ./Dockerfile /home/<USER>/workdir/
```
This will copy the Dockerfile in the current directory on your local machine to the `/home/<USER>/workdir/` directory in the Docker image.

## Copying Files to the Container
You can also copy without modifying the Dockerfile:
```bash
touch example_local_file.txt
echo "This is an example file produced on the local host." > example_local_file.txt
docker cp example_local_file.txt <container_id>:/home/<USER>/workdir/
```
- If you encounter permission issues you can change the permissions of the file by running:
```bash
chmod a+w example_local_file.txt
```
- You can also copy files from the container to your local machine by running:
```bash
docker cp <container_name>:/home/<USER>/workdir/example_local_file.txt .
```

## Mounting a Local Directory/Volume
You can also mount a local directory to the container by running:
```bash
docker run -it -v /path/on/local/dir:/path/on/container <container_name>
```
This is particularly useful for sharing files between the host and the container. In other words, it allows for direct access to the host file system from within the container and for processes running in the container to write directly on the host file system.


## Exercises:
1. Pull the minilinux image from Docker Hub by copying the command from the Docker Hub page. Search for the image `tkardocker/docker-git-intro` on Docker Hub.
2. Run the image and check if it works.
3. Modify the Dockerfile to install a different version of Python and add a few additional packages, for e.g. numpy, matplotlib, pandas, and jupyter using pip. For this, you will have to first install pip. You can do this by running the following command:
```bash
apt-get install -y python3-pip
```
4. Build the image and run it.
5. Copy a file from your local machine to the container and check if it works.
6. Copy a file from the container to your local machine and check if it works.
7. Mount a local directory to the container from the command line and try writing a file to it.
8. Modify your dockerfile to also install git. Build and run the image and check if git is installed by running:
```bash
git --version
```

## Bonus: Pushing to Docker Hub
You have to first create an account on Docker Hub. After that, you should go to your terminal and create a gpg key by running:
```bash
gpg --generate-key
```
You will be prompted to enter your name and email address. Make sure to use the same email address you used to create your Docker Hub account. After that, you can run the following command to export your public key:
```bash
gpg --list-keys
```
Then copy the large string of numbers and letters after pub and paste it as <public_key> in the following command:
```bash
pass init <public_key>
```
Now you can login to Docker Hub with your Docker Hub credentials by running:
```bash
docker login -u <your_docker_hub_username>
```
Enter your password when prompted. If you have two-factor authentication enabled, you will need to generate a personal access token and use that as your password. You can generate a personal access token by going to your Docker Hub account settings.

After that, you can push your image to Docker Hub by running:
```bash
docker tag <image_id> <your_docker_hub_username>/<image_name>:<tag>
docker push <your_docker_hub_username>/<image_name>:<tag>
```
You can also pull the image from Docker Hub by running the following command or search for it on Docker Hub:
```bash
docker pull <your_docker_hub_username>/<image_name>:<tag>
```