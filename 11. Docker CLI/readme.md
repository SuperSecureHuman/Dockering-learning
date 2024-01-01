# Docker Command Line

The Docker Command Line Interface (CLI) is a tool that lets you talk to and manage Docker containers, images, volumes, and networks. Here's a simple guide to get you started:

## 1. Installation

Before you can use Docker CLI, you need to have Docker installed on your computer. You can get it from the official Docker website.

## 2. Basic Commands

Here are some important basic Docker CLI commands you should know:

- `docker run`: This command creates and starts a container from a Docker image
- `docker container`: This command shows running containers
- `docker image`: This command lists all images on your system
- `docker pull`: This command gets an image from Docker Hub or another registry
- `docker push`: This command sends an image to Docker Hub or another registry
- `docker build`: This command creates an image from a Dockerfile
- `docker exec`: This command runs a command in a running container
- `docker logs`: This command shows the logs of a container

## 3. Docker Run Options

The `docker run` command is really important. You can use different options with `docker run` to customize the container:

- `-d, --detach`: This option runs the container in the background
- `-e, --env`: You can use this option to set environment variables for the container
- `-v, --volume`: You can use this option to link a volume
- `-p, --publish`: This option publishes the container's port to the host
- `--name`: You can use this option to give the container a name
- `--restart`: This option sets the container's restart policy
- `--rm`: This option gets rid of the container when it exits

## 4. Dockerfile

A Dockerfile is a script that has instructions to make a Docker image. A Dockerfile looks something like this:

```dockerfile
# Choose the base image
FROM alpine:3.7

# Update the system and install software packages
RUN apk update && apk add curl

# Decide the working directory
WORKDIR /app

# Copy the application file
COPY app.sh .

# Choose the entry point
ENTRYPOINT ["./app.sh"]
```

To make the image, you would use the following command:

```bash
docker build -t my-image .
```

## 5. Docker Compose

Docker Compose is a CLI tool that lets you manage multi-container Docker applications. You can install Docker Compose from the official Docker website and then you can create a `docker-compose.yml` file to define and run multiple containers:

```yaml
version: '3'
services:
  web:
    image: webapp-image
    ports:
      - "80:80"
  database:
    image: mysql
    environment:
      - MYSQL_ROOT_PASSWORD=my-secret-pw
```

To run the application, use the following command:

```bash
docker-compose up
```

## Docker Images

Docker images are lightweight, standalone, and executable packages that include everything needed to run an application. These images contain all necessary dependencies, libraries, runtime, system tools, and code to enable the application to run consistently across different environments.

Docker images are built and managed using Dockerfiles. A Dockerfile is a script that consists of instructions to create a Docker image, providing a step-by-step guide for setting up the application environment.

Some important docker commands when working with Docker images include:

- `docker image ls`: This command lists all images on your local system.
- `docker build`: This command creates an image from a Dockerfile.
- `docker image rm`: This command gets rid of an image.
- `docker pull`: This command gets an image from a registry (like Docker Hub) to your local system.
- `docker push`: This command sends an image to a repository.

### Sharing Images

Docker images can be shared and distributed using container registries, such as Docker Hub, Google Container Registry, or Amazon Elastic Container Registry (ECR). Once your images are pushed to a registry, others can easily access and utilize them.

To share your image, you first need to tag it with a proper naming format:

```bash
docker tag <image-id> <username>/<repository>:<tag>
```

Then, you can push the tagged image to a registry using:

```bash
docker push <username>/<repository>:<tag>
```

## Containers

Containers can be thought of as lightweight, stand-alone, and executable software packages that include everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and config files. Containers isolate software from its surroundings, ensuring that it works uniformly across different environments.

### Why Use Containers?

- **Portability**: Containers ensure that applications work consistently across different platforms, be it a developer's laptop or a production server. This eliminates the "it works on my machine" problem.

- **Efficiency**: Containers are lightweight since they use shared resources without the overhead of a full-fledged operating system. This enables faster startup times and reduces resource usage.

- **Scalability**: Containers can be effortlessly scaled up or down according to the workload, making it ideal for distributed applications and microservices.

- **Consistency**: Containers enable developers, QA, and operations teams to have a consistent environment throughout the application lifecycle, leading to faster and smoother deployment pipelines.

- **Security**: Containers provide a level of isolation from other containers and the underlying host system, which aids in maintaining application security.

### Working with Containers using Docker CLI

Docker CLI offers several commands to help you create, manage, and interact with containers. Some common commands include:

- `docker run`: Used to create and start a new container.

- `docker container ls`: Lists running containers.

- `docker container stop`: Stops a running container.

- `docker container rm`: Removes a stopped container.

- `docker exec`: Executes a command inside a running container.

- `docker logs`: Fetches the logs of a container, useful for debugging issues.

## Docker Volumes

Docker volumes are efficient ways to store information from Docker containers. They allow you to keep data separate from the container, making it easier to back up or move data.

### Why Volumes Matter

Docker containers can be easily stopped, deleted, or replaced. This doesn't work out well when needing to hang on to data, though. Volumes solve this problem by providing a method to separately store and manage data from the container's lifespan.

### Types of Volumes

Docker has three types of volumes:

- **Host Volumes**: Stored on the host computer's file system, usually in the `/var/lib/docker/volumes` directory. Easy to access, but can cause issues with moving data around or file system compatibility.

- **Anonymous Volumes**: These are automatically created when a container is run and no volume is specified. Their ID is Docker-generated and they're also stored on the host computer's file system.

- **Named Volumes**: Like anonymous volumes, they're stored on the host computer's file system. However, you can assign a custom name, making it simple to reference in other containers or for backups.

### Managing Volumes with Docker Commands

Docker commands help manage volumes:

- `docker volume create`: Make a new volume with a specified name.
- `docker volume ls`: Lists all volumes on the system.
- `docker volume inspect`: Gives detailed information about a specific volume.
- `docker volume rm`: Removes a volume.
- `docker volume prune`: Deletes all unused volumes.

When starting a container, use the `-v` or `--volume` flag to use a volume. For example:

```bash
docker run -d --name my-container -v my-named-volume:/var/lib/data my-image
```

This starts a new container named "my-container" using the "my-image" image. The "my-named-volume" volume is mounted at the `/var/lib/data` path inside the container.

## Networking with Docker

Docker networks are superb for allowing containers to communicate. It permits containers to interact with each other and the host machine via different network drivers. By knowing and using varying types of network drivers, you can build networks to handle specific needs or app requirements.

## Network Drivers

Several network drivers are available in Docker. The four most used ones are:

- **bridge**: The standard network driver for containers. Creates a private network where containers can interact with each other and the host machine. Containers on this network can access outside resources via the host's network.
- **host**: This driver lifts network isolation and lets containers use the host's network. Useful in situations where network performance is key, as it reduces the overhead of container networking.
- **none**: This network driver turns off container networking. Containers employing this driver operate in an isolated environment with no network access.
- **overlay**: This network driver lets containers on different hosts interact with each other. It's designed for use with Docker Swarm and is ideal for multi-host or group-based container setups.

## Managing Docker Networks

Docker commands can manage networks:

- List all networks: `docker network ls`
- Scrutinise a network: `docker network inspect <network_name>`
- Create a new network: `docker network create --driver <driver_type> <network_name>`
- Connect containers to a network: `docker network connect <network_name> <container_name>`
- Disconnect containers from a network: `docker network disconnect <network_name> <container_name>`
- Delete a network: `docker network rm <network_name>`
