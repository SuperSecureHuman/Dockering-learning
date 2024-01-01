# Docker Basics

## Components

There are three key components in the Docker ecosystem:

**Dockerfile:** A text file containing instructions (commands) to build a Docker image.
**Docker Image:** A snapshot of a container, created from a Dockerfile. Images are stored in a registry, like Docker Hub, and can be pulled or pushed to the registry.
**Docker Container:** A running instance of a Docker image.

## Some commands to remember/refer

`docker pull <image>`: This command downloads an image from a registry (for example, Docker Hub).

`docker build -t <image_name> <path>`: This command builds an image from a Dockerfile. Here, `<path>` is the directory that has the Dockerfile.

`docker image ls`: This command lists all the images that are currently available on your computer.

`docker run -d -p <host_port>:<container_port> --name <container_name> <image>`: This command runs a container from an image and maps the ports of the host to the container ports.

`docker container ls`: This command lists all the containers that are currently running.

`docker container stop <container>`: This command stops a container that is currently running.

`docker container rm <container>`: This command removes a container that has been stopped.

`docker image rm <image>`: This command removes an image from your computer.
