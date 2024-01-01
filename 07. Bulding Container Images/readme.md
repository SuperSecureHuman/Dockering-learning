# Dockerfile

A Dockerfile is a basic text file that has a list of tasks. Docker engines, the heart of Docker, use these tasks to create an image. Each task adds a layer to the image. Docker creates the image based on these tasks and then you can create containers from this image. Dockerfiles are vital parts of *software setups*.

## Structure of a Dockerfile

A Dockerfile is organized into different instructions or tasks. There is one instruction per line. Each instruction has a certain method.

```bash
INSTRUCTION arguments
```

Below is a basic Dockerfile, as an example:

```bash
# Use official Python resource for the base
FROM python:3.7-slim

# Create a working directory called '/app'
WORKDIR /app

# Duplicate your current directory into the '/app' directory in the container 
COPY . /app

# Install any requirements you specified
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Let others access port 80 outside of this container
EXPOSE 80

# Create environment variable
ENV NAME World

# Run app.py when the container starts
CMD ["python", "app.py"]
```

## Common Dockerfile Tasks

Here are some common Dockerfile tasks and what each one does:

- `FROM`: Sets the base image you'll work off of. `FROM` has to be the first rule in the Dockerfile.
- `WORKDIR`: Sets the directory that all `RUN`, `CMD`, `ENTRYPOINT`, `COPY` or `ADD` tasks will occur in. If the directory doesn't exist, Docker will create it.
- `COPY`: Copies things from your computer into the container's file system.
- `ADD`: Similar to `COPY`, but it can also access remote URLs and open up archives.
- `RUN`: Executes a task as a new layer in the image.
- `CMD`: Specifies the default command that will be run when a container is created from the image.
- `ENTRYPOINT`: Similar to `CMD`, but it's designed so that a container works as an executable with its own parameters.
- `EXPOSE`: Lets Docker know that the container will listen to certain network ports once it's running.
- `ENV`: Creates environment variables for the container.

## Building an Image from a Dockerfile

To create an image from a Dockerfile, you use the command `docker build`, specifying the method (usually your current directory), and a possible tag for the image.

```bash
docker build -t my-image:tag .
```

After running this command, Docker will execute each rule you listed in the Dockerfile, in order. Each instruction will create a new layer.

## Looking at Images and Layers

After a successful build, you can look at the image you made using `docker image` command:

```sh
docker image ls
```

Want to view the individual layers of an image? Use the `docker history` command:

```sh
docker history name-for-your-image
```

You can also use the `docker inspect` command to see the layers of an image:

```sh
docker inspect name-for-your-image
```

To delete an image, use the `docker image rm` command:

```sh
docker image rm name-for-your-image
```

## Sending Images to a Registry

After making your image, you can send it to a container registry (like Docker Hub, Google Container Registry, etc.) to share and use your application easily. First, log in to the registry with your user details:

```sh
docker login
```

Then, tag your image with the URL of the registry:

```sh
docker tag name-for-your-image username/repository:tag
```

Last, push the tagged image to the registry:

```sh
docker push username/repository:tag
```

Making container images is a central part of using Docker, as it lets you package and launch your applications simply. By making a Dockerfile with clear instructions, you can make and share images across any platform without trouble.

## Making Docker Faster With Layer Caching

When Docker is creating container images, it saves (or "caches") the new layers it forms. Later, when creating other images, it can use the layers it saved before. This helps speed things up and also uses less data. But, to get the most from this caching process, you need to know how to use layer caching well.

### Understanding Docker Layer Caching

With every instruction given in the Dockerfile (like `RUN`, `COPY`, `ADD`, etc.), Docker makes a new layer. If the same instruction is used again, Docker uses the layer it created before.

Take a look at this Dockerfile example:

```dockerfile
FROM node:14

WORKDIR /app

COPY package.json /app/
RUN npm install

COPY . /app/

CMD ["npm", "start"]
```

The first time you build an image from this Dockerfile, Docker will produce a new layer for every instruction. Now, if you change your application and build a new image, Docker will only create new layers for the instructions changed. If no changes are made in the instructions, it will use the layers it saved before.

### How to Make Layer Caching More Efficient

- **Limit Dockerfile changes:** By making fewer changes to your Dockerfile and arranging your instructions so that the most frequently changed lines are last.

- **Optimize build context:** Use a `.dockerignore` file to stop unnecessary files from interrupting the caching process.

- **Prefer smaller base images:** Using smaller base images is quicker and means fewer layers need to be cached.

- **Use Docker's `--cache-from` feature:** If you're using a CI/CD pipeline, this feature lets you choose which image to use for caching.

- **Combine multiple instructions:** Combining instructions (like `RUN`) can reduce the number of layers making caching quicker.

By following these tips, you can make your Docker images build faster and use less space. This way, you can speed up your work and make the whole process much more efficient.

- [Docker Layer Caching](https://docs.docker.com/build/cache/).


## Making Images Compact and Secure

When you're building your container images, paying attention to the size and the security of the image is crucial. If your image is small, your containers will be assembled and launched faster. Also, less data will need to be sent over the network when the image is downloaded. Security is another important aspect as the content of containers can sometimes create potential risks for your applications.

### Making Images Smaller

- **Choose an appropriate base image:** Going for a base image that's compact and has only the components your application needs can help. For example, using the 'alpine' version of the base image (if it's available) is often a good idea because it tends to be much smaller.

    ```dockerfile
    FROM node:14-alpine
    ```

- **Group commands in the `RUN` statement:** Every `RUN` statement you use creates a fresh layer in the image, which makes the image larger. To minimise the number of layers and therefore make the final image smaller, try to group commands in a single `RUN` statement using '&&'.

    ```dockerfile
    RUN apt-get update && \
        apt-get install -y some-required-package
    ```

- **Remove unwanted files in each layer:** Any files added or installed during the image build process that aren't needed should be removed within the same layer to help keep the final image size down.

    ```dockerfile
    RUN apt-get update && \
        apt-get install -y some-required-package && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*
    ```

- **Use multi-stage builds:** Multi-stage builds can make images smaller. These allow you to use several 'FROM' statements in your Dockerfile. Each one creates a different stage of the build process. Files can then be moved from one stage to another with the 'COPY --from' statement.

    ```dockerfile
    FROM node:14-alpine AS build
    WORKDIR /app
    COPY package*.json ./
    RUN npm install
    COPY . .
    RUN npm run build

    FROM node:14-alpine
    WORKDIR /app
    COPY --from=build /app/dist ./dist
    COPY package*.json ./
    RUN npm install --production
    CMD ["npm", "start"]
    ```

- **Use a `.dockerignore` file:** This file will prevent unneeded files from being included in the build, preventing unnecessary increases in the final image size.

    ```
    node_modules
    npm-debug.log
    ```

### Maximising Security

- **Keep base images updated:** It's a good idea to regularly refresh the base images used in your Dockerfiles. This ensures they include the most recent security updates.

- **Avoid running containers as root:** Try to use a non-root user whenever possible when running containers. This reduces potential risks. Create a user and switch to it before setting your application running.

    ```dockerfile
    RUN addgroup -g 1000 appuser && \
        adduser -u 1000 -G appuser -D appuser
    USER appuser
    ```

- **Limit the range of `COPY` or `ADD` instructions:** Be careful about which folders or files you're copying to the container image. It's a good idea to avoid using 'COPY . .' as this might accidentally include sensitive files.

    ```dockerfile
    COPY package*.json ./
    COPY src/ src/
    ```

- **Scan for vulnerabilities in images:** Use tools such as [Anchore](https://anchore.com/) or [Clair](https://github.com/quay/clair) to scan your images for any potential vulnerabilities. Fix these before you deploy anything.

By following these best practices, you can build container images that are both efficient and secure. This leads to better performance and reduced risks when deploying your applications.
