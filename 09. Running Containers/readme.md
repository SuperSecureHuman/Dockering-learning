# Running Containers

To start a new container, you use the command `docker run` together with the name of the image you want to run. Here's a simple example using the official Nginx image:

```bash
docker run -d -p 8080:80 nginx
```

## Few commands to get started

This command tells Docker to start a new container using the Nginx image, running in the background (`-d`) and connecting the host's port 8080 to the container's port 80.

### Seeing Your Containers

To see a list of all your running containers, use the `docker ps` command. If you want to see all your containers, even the ones that aren't running, add the `-a` option:

```bash
docker container ls -a
```

### Interacting with Containers

If you want to access a running container, you can use the `docker exec` command together with the container's ID:

```bash
docker exec -it CONTAINER_ID bash
```

The `docker ps` command will give you the ID of your container.

### Stopping Containers

To stop a running container, all you need is the `docker stop` command followed by the container's ID or name:

```bash
docker container stop CONTAINER_ID
```

### Deleting Containers

Once you're done with a container, you can remove it using the `docker rm` command:

```bash
docker container rm CONTAINER_ID
```

You can also decide to remove the container automatically once it exits by using the `--rm` option with the `docker run` command:

```bash
docker run --rm IMAGE
```

## There is more to  `docker run`

The command `docker run` lets you run Docker containers. It starts a new container from the specified image.

Here's the basic usage:

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

A few pointers:

- `OPTIONS`: these are command flags that let you change the container's settings.
- `IMAGE`: this is the Docker image the container is running from.
- `COMMAND`: the command to run when the container starts. If you don't specify a command, the image's default command will be used.
- `ARG...`: these are optional arguments for the command.

### Some Extra Options

Here are a few extra options for the `docker run` command:

- `--name`: gives the container a name.
- `-p, --publish`: publish a container's port to the host.
- `-e, --env`: set environment variables in the container. You can use this multiple times for different variables.
- `-d, --detach`: run the container in the background.
- `-v, --volume`: make a link from the container to a location on the host.

### Some Examples

Here are a few examples of the `docker run` command:

- Start an interactive session of an Ubuntu container:

```bash
docker run -it --name=my-ubuntu ubuntu
```

- Run an Nginx web server and publish the port 80 on the host:

```bash
docker run -d --name=my-nginx -p 80:80 nginx
```

- Run a MySQL container with a custom environment variable for configuring the database:

```bash
docker run -d --name=my-mysql -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=mydb -p 3306:3306 mysql
```

- Run a container with a volume:

```bash
docker run -d --name=my-data -v /path/on/host:/path/in/container some-image
```

## Docker Compose

Docker compose is a tool to start and manage multiple Docker containers at the same time. In a `docker-compose.yml` file, you can describe all the containers you need, together with their settings. This file makes it easy to set up and manage complex applications.

Advantages of Docker compose include easy container management and reproducible builds.

### Creating a Docker Compose File

A `docker-compose.yml` file starts with the version of Docker compose you are using, followed by the services you want to define. Here's an example of a basic `docker-compose.yml` file:

```yaml
version: "3.9"
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: mysecretpassword
```

### Running Docker Compose

To start your Docker compose application, open a terminal in the directory containing your `docker-compose.yml` file and run:

```bash
docker-compose up
```

Docker Compose will start up all the containers defined in the file.

### Other Useful Commands

- `docker-compose down`: Stop and remove all of the containers defined in the `docker-compose.yml` file.
- `docker-compose ps`: Check the status of the containers defined in the `docker-compose.yml` file.
- `docker-compose logs`: Show the logs of the containers defined in the `docker-compose.yml` file.
- `docker-compose build`: Build the images defined in the `docker-compose.yml` file.

## Adjusting Container Settings

When running your containers, you have a bunch of options that let you alter the container's behaviour and resources. Here's a brief overview of some commonly used options:

### Resource Management

- **CPU:** You can limit a container's CPU usage with the `--cpus` and `--cpu-shares` options. `--cpus` limits the number of CPU cores a container can use, and `--cpu-shares` sets a share of CPU time for the container.

- **Memory:** You can limit and reserve memory for a container using the `--memory` and `--memory-reservation` options.

### Security

- **User:** By default, containers run as the `root` user. For added security, you can use the `--user` option to run a container as a different user.

- **Read-only root file system:** You can use the `--read-only` option to stop unwanted changes to the container file system.

### Networking

- **Publish Ports:** You can use the `--publish` (or `-p`) option to make a container's ports available to the host system.

- **Hostname and DNS:** You can customize the container's hostname and DNS settings using the `--hostname` and `--dns` options.

There are many more options available, so be sure to check Docker's [official documentation](https://docs.docker.com/engine/reference/run/) for more information on adjusting runtime configuration.
