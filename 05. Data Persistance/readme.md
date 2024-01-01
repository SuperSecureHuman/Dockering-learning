# Storing Data in Docker

When we talk about containers, they're generally temporary. This means that data within a container doesn't stick around when the container is stopped or removed. For most apps, data needs to be stored for them to work. So, let's look at how Docker containers can keep data.

## Ephemeral FS

A Docker container is meant to be temporary and doesn't naturally keep information. By default, the storage inside a Docker container is short-lived, meaning any changes made inside the container will only stick around as long as the container is active. Once the container is stopped and removed, all the data associated with it is lost.

### Ephemeral FS and Data Persistence

There's a problem with short-lived storage for applications like databases, which need data to stick around longer than the life of one container. Docker has some ways to make sure data keeps:

* **Volumes:** A Docker managed storage option, stored outside the container’s filesystem, allowing data to survive container restarts and removals.
* **Bind mounts:** Mapping a host machine’s directory or file into a container, effectively sharing the host’s storage with the container.
* **Tmpfs mounts:** In-memory storage, useful for cases where just the persistence of data within the life-cycle of the container is required.

![Image](https://i.imgur.com/Agh3gHa.png)

Think about two teams, one working with data and one creating models. Ideally, you'd want a shared place both teams can access data and models. This is where 'Docker volumes’ come into play. A Docker volume is a folder on the host machine that Docker uses to store files and folders, outlasting the life of the container. Docker volumes can be shared between containers and make things like backups and data transfers easy.

## Docker Volumes

To create a volume, use the `docker volume create` command. For example, you can create a volume called 'my_volume':

```bash
docker volume create my_volume
```

To see all the volumes on your computer, you can use the `docker volume ls` command:

```bash
docker volume ls
```

You can inspect a volume using the `docker volume inspect` command:

```bash
docker volume inspect my_volume
```

To remove a volume, you can use the `docker volume rm` command:

```bash
docker volume rm my_volume
```

To use a volume in a container, we use the '-v' flag when running the container. For example, to run a container with a volume called 'my_volume':

```bash
docker run -d -p 5000:5000 -v my_volume:/data --name my_container my_image
```

### Sharing Volumes Between Containers

To share a volume between multiple containers, simply mount the same volume on multiple containers. Here’s how to share my-volume between two containers running different images:

![Image](https://i.imgur.com/eRYSAUg.png)

```bash
docker run -d -v my-volume:/data1 image1
docker run -d -v my-volume:/data2 image2
```

In this example, image1 and image2 would have access to the same data stored in my-volume.

[Read More - Docker Docs](https://docs.docker.com/storage/volumes/)

## Bind Mounts

Bind mounts let you map any folder on the main computer to a folder within the container. This can be handy in development environments where you need to tweak files on the main system, and you want those changes to be available within the container immediately. Bind mounts are also a good way to share files between the main machine and the container. Even if you delete the container, the bind mount still exists on the main machine.

To use a bind mount, we use the '-v' flag when running the container. For example, to run a container with a bind mount:

```bash
docker run -d -p 5000:5000 -v /home/user/data:/data --name my_container my_image
```

Here, '/home/user/data' is the directory on the host machine, and '/data' is the directory within the container.

[Read More - Docker Docs](https://docs.docker.com/storage/bind-mounts/)

## Docker tmpfs mounts

Docker tmpfs mounts provide temporary, in-memory filesystems that are created inside containers. This means that the data stored in a tmpfs mount never gets written to the disk. It can be used for storing sensitive data that you don't want to save to disk, or for apps that need quick I/O.

To use a tmpfs mount, we use the '--tmpfs' flag when running the container. For example, to run a container with a tmpfs mount:

```bash
docker run -d -p 5000:5000 --tmpfs /data --name my_container my_image
```

Docker volumes, bind mounts, and Docker tmpfs mounts are all different ways to store data in Docker containers. Docker volumes are the most commonly used method, with benefits like easy backups and data migration. Bind mounts are useful in development environments, and Docker tmpfs mounts are useful for sensitive data and quick I/O needs.
