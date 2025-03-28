# Prerequisites Installation
This section provides instructions for installing the prerequisites for the course. The prerequisites include:
- Docker Engine/ Docker Desktop

If something is unclear or you encounter any issues, please contact the course instructor.
## MacOS users
MacOS users are recommended to install Docker Desktop for Mac. The instructions for the same can be found [here](https://docs.docker.com/desktop/mac/install/).
Post installation of Docker Desktop, proceed with the verification steps mentioned in [Verify Docker installation](#verify-that-docker-engine-is-installed-correctly-by-running-the-hello-world-image).
## Linux users
If you use Ubuntu as your linux distribution you can jump to the [Docker Engine Installation on Ubuntu](#docker-engine-installation-on-ubuntu) section. 
Instructions for other Linux distributions can be found [here](https://docs.docker.com/engine/install/).
## Windows users
It is recommended to install `Windows Subsystem for Linux` (WSL) and use the Ubuntu terminal for this course if you are a windows user.
### Windows Subsystem for Linux (WSL) installation
A summary of the install instructions from the following [reference](https://learn.microsoft.com/en-us/windows/wsl/setup/environment) is given below:
- Open PowerShell (or Windows Command Prompt) and enter:

```powershell
wsl --install
```
- You will be prompted to enter a `username` and `password` for your Linux distribution. This username and password will be used to install and configure software on your Linux distribution.
- Note that while entering password nothing will appear on the screen. If prompted to restart your computer, restart it.
- After installation, you can open the Ubuntu terminal by searching for `Ubuntu` in the Windows search bar or just typing `wsl` in the command prompt/powershell.
```powershell
wsl
```
- You can now proceed with the following steps in the Ubuntu terminal.
This might take a while depending on your internet connection speed.
```bash
sudo apt update && sudo apt upgrade
```
- You can now install Docker Engine on Ubuntu. The instructions for the same are given below.

### Docker Engine Installation on Ubuntu
Note that we will be using the terminal and hence you are recommended to install docker engine on Ubuntu or any other linux distribution. You can also install docker desktop for Windows. The instructions for the same can be found [here](https://docs.docker.com/get-docker/).

Below is a summary of the installation instructions for Ubuntu. 

- Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```bash
sudo apt-get install \
     ca-certificates \
     curl \
     gnupg \
     lsb-release 
```
- Add Docker’s official GPG key:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
- Add repository to Apt sources:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- Update the package index, and install the latest version of Docker Engine and containerd:
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### Verify that Docker Engine is installed correctly by running the `hello-world` image:
Open a terminal and run the following commands. MacOS users should open the installed Docker Desktop Application before executing the following commands in their terminal.
- Pull a Docker image from Docker Hub by running:
```bash
sudo docker pull hello-world
```
- Run the Docker image by running:
```bash
sudo docker run hello-world
```
- If you are unable to run the `hello-world` image, you might need to start the Docker service. MacOS users can do this by typing `docker open` in the terminal. Linux users can start the Docker service by running:
```bash
sudo systemctl start docker
```
- You can also check the status of the Docker service by running:
```bash
sudo systemctl status docker
```
- If none of the above steps work, you can check if your user is part of the `docker` group by running:
```bash
groups
```
- If your user is not part of the `docker` group, you can add it by running:
```bash
sudo usermod -aG docker $USER
```
- You will need to log out and log back in for the changes to take effect.
- You can now proceed with the Docker commands mentioned in the [Docker Introduction](../docker/README.md) section.
