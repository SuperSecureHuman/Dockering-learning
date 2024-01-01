# Underlying Technologies

There are some stuff you need to understand before you can fully grasp the concept of Docker.

## Linux Containers (LXC)

Linux Containers (LXC) are the base layer for Docker. LXC is a straightforward virtualization method that allows multiple separate Linux systems to operate on a single host without requiring a complete hypervisor. LXC efficiently isolates applications with their needs in a safe and well-optimized way.

![LXC vs Docker](https://i.imgur.com/lbT37EN.png)

## Control Groups (cgroups)

Control Groups, or simply cgroups, is a clever feature in Linux that lets you control the resources such as the computer power, memory, and data control for groups of processes. Docker uses cgroups to regulate the resources used by 'containers' to prevent any one container from gobbling up all the system's resources.

Docker utilizes cgroups to enforce resource constraints on containers, allowing them to have a consistent and predictable behavior. Below are some of the key features and benefits of cgroups in the context of Docker containers:

**Resource Isolation:** cgroups stops each container from using too many resources which could slow down other containers.

**Limiting Resources:** Using cgroups, you can limit the amount of different system resources each container uses.

**Prioritizing Containers:** cgroups allows you to decide the importance of each container and allocate resources accordingly.

**Monitoring:** cgroups lets you keep track of each container's resource usage, which can help identify any issues or bottlenecks.

So - cgroups play a big part in how Docker operates by keeping an eye on resources and ensuring things run smoothly.

## Union File Systems (UnionFS)

Union File Systems, or UnionFS, is a really key part of how Docker works. Basically, it's a special way of managing files that lets you layer multiple directories on top of each other without merging them. This is important in Docker since it keeps storage neat and prevents unnecessary duplication.

These are some of the essential features of union filesystems:

Key features of union filesystems include:

**Layered Structure:** UnionFS manages changes really well by only updating the top, changeable layer - the original data stays untouched.
**Copy-on-Write:** If a container alters a file, the system makes a copy in the top layer, leaving the original untouched.
**Resource Sharing:** Union filesystems let containers that share common elements run separately, saving space.
**Fast Container Initialization:** Union filesystems allow new containers to be created instantly, which improves performance.

There are a few popular Union Filesystems used in Docker. These include AUFS, OverlayFS, Btrfs and ZFS. Each has its strengths and is used for different things.

## Namespaces

Namespaces are a really important feature in Linux as they keep different processes separated. Docker uses namespaces to make its containers. Each container has its own set of namespaces which keep the processes within it separate from processes outside of it.

There are several types of namespaces in Linux, including:

**PID (Process IDs):** Isolates the process ID number space, which means that processes within a container only see their own processes, not those on the host or in other containers.
**Network (NET):** Provides each container with a separate view of the network stack, including its own network interfaces, routing tables, and firewall rules.
**Mount (MNT):** Isolates the file system mount points in such a way that each container has its own root file system, and mounted resources appear only within that container.
**UTS (UNIX Time Sharing System):** Allows each container to have its own hostname and domain name, separate from other containers and the host system.
**User (USER):** Maps user and group identifiers between the container and the host, so different permissions can be set for resources within the container.
**IPC (Inter-Process Communication):** Allows or restricts the communication between processes in different containers.

When Docker starts a container, it creates a new set of namespaces for that container. These only apply within the container, which means processes inside a specific container only have access to a certain subset of system resources.

In short, Docker uses namespaces to manage resources and keep containers separate. This forms a key part of Docker’s container technology.

## Read more

[Docker vs LXC](https://dockerlabs.collabnix.com/beginners/docker/docker-vs-container.html)
