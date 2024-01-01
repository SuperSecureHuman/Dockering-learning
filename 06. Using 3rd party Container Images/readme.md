# Using Third-Party Docker Images

Third-party images are ready-made Docker container images available on repositories like Docker Hub or other sites. They're made and kept up to date by people or groups and can be a great starting point for your containerized apps.

A great example of a third-party Docker image is the nvidia/cuda image. NVIDIA looks after this image, and it's used to run apps on a Graphics Processing Unit (GPU) inside a container. You can easily recreate the environment on different machines without spending too much time installing all the software it needs.

Docker Hub is the go-to storage place for Docker images. It has a huge number of images that are free to use. You can also make your own images and make them available on Docker Hub.

[Docker Hub](https://hub.docker.com/search)

Using these Docker images as a base for your images is just as easy as using the official images. You can use the `FROM` command to state the base image for your image.

```dockerfile
FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04

# # # Rest of your Dockerfile # # #
```

## Be Careful of Security

Keep an eye on security when using third-party images. They could have security weaknesses or be set up wrongly. Always check the source of the image and its reputation before using it in your final product. Try to use official images or community images that are well-maintained.

## Looking After Your Images

When you use third-party images, it's important to keep them up-to-date. This ensures the latest security updates and software changes are included. Regularly check for updates in your base images and rebuild your application containers if needed.
