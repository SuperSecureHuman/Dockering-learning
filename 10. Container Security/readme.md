# Container Safety

To use Docker and similar technologies correctly and smartly, it's essential that we focus on container safety. This is all about using the right practices, tools and technologies to keep our apps and the system they work on safe. Let's look at a few key things we need to do to ensure this.

## Keeping Containers Separate

It's really important to keep our containers separate from each other and from the main system. This minimises any damage done if someone breaks into your container.

Docker uses namespaces to create safe environments for running containers, and cgroups to manage how much resources each container uses.

**Namespaces:** Docker uses namespace technology to provide isolated environments for running containers. Namespaces restrict what a container can see and access in the broader system, including process and network resources.

**Cgroups:** Control groups (cgroups) are used to limit the resources consumed by containers, such as CPU, memory, and I/O. Proper use of cgroups aids in preventing DoS attacks and resource exhaustion scenarios.

## Safe Habits and Practices

Sticking to best practices and particular safety habits is key in maintaining a secure system.

**Least Privilege:** Only give your containers bare minimum access rights.

**Immutable Infrastructure:** Don't alter your containers once built. If you want to make changes, create a new container.

**Version Control:** Keep your images under version control and store them safely.

## Secure Controls

Apply secure controls to both the management of your containers and the data within them.

**Managing Containers:** Follow the Role-Based Access Control (RBAC) rule to restrict who can do what with your containers.

**Container Data:** Always encrypt your data whether it's at rest or on the move - the more sensitive the data, the more protection it needs.

## Looking for Vulnerabilities

Containers can sometimes be vulnerable to attack. It's crucial to use good management to safeguard against this.

**Image Scanning:** Use automated services to find any vulnerabilities in your containers and images.

**Secure Base Images:** When making a container, use images with minimal and secure base.

**Regular Updates:** Always keep your images and containers up to date with the latest security patches.

By understanding and following these container security principles, you can make sure your applications and infrastructure are safe against threats.

## Image Security

Safety extends to image security too - it's really important when using Docker to make sure your images are secure, current and fault-free.

**Use Trusted Image Sources:** Always use trusted, official images when pulling from public repositories.

**Keep Images Up-to-Date:** Monitor your images and keep them updated regularly.

**Use Minimal Base Images:** A minimal base image is a bare-bones version that has only what's needed to run a containerized app. The fewer components, the fewer chances for vulnerabilities.

**Scan Images for Vulnerabilities:** Scan your images for known vulnerabilities regularly.

**Sign and Verify Images:** Sign your images with Docker Content Trust (DCT) to ensure their integrity and authenticity.

**Use Multi-Stage Builds:** Multi-stage builds let you use multiple FROM instructions within the same Dockerfile, reducing the risk factor of vulnerabilities.

If you follow these practices, you can minimise risk and make sure your applications are safe.

## Keep it Safe in Real Time

Runtime security is all about keeping Docker containers safe while they're running.

**Least Privilege Principle:** Make sure your containers follow the principle of least privilege.

**Read-only Filesystems:** Setting your filesystems to read-only prevents hackers from modifying files or defending malware inside your containers.

**Security Scanning and Monitoring:** Monitor your containers for vulnerabilities both in the images and in the runtime environment.

**Resource Isolation:** Keep your resources isolated to avoid any compromised container affecting others or the system.

**Audit Logs:** Maintain audit logs of container activity that can help with identifying, troubleshooting and complying with security measures.

Runtime security is all about making sure your Docker containers stay safe, even after being deployed in your system.
