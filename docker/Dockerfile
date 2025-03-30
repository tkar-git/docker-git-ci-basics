#Dockerfile
# This Dockerfile sets up a basic environment for Python development with Jupyter Notebook
# and includes the necessary packages for data analysis and visualization.

# Start with a basic Ubuntu image
FROM ubuntu:latest

# Build the image as a root user
USER root

ARG USERNAME=docker

# Prevent interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install Python and Git
RUN apt-get -y update  && \
    apt-get -y upgrade && \
    apt-get -y install sl && \
    apt-get install -y python3 && \
    apt-get -y autoclean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* && \
    ln -s /usr/games/sl /usr/bin/sl 

# Add a user to the image
RUN useradd -m ${USERNAME}

# Set a working directory for the container
WORKDIR /home/${USERNAME}/my_workdir/

COPY ./Dockerfile /home/${USERNAME}/my_workdir/
RUN chown ${USERNAME}:${USERNAME} /home/${USERNAME}/my_workdir/Dockerfile

# Set the default command to run when the container starts
CMD ["bash"]

# Run as docker user by default when the container starts up
USER ${USERNAME}