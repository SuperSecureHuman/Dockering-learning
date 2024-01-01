# Making use of Third-Party Docker Images: Databases

Running your database in a Docker container can make your development process faster and make deployment easier. Docker Hub offers numerous ready-made images for popular databases such as MySQL, PostgreSQL, and MongoDB.

Example: MySQL Image
To start with a MySQL database, search for the official image on Docker Hub:

```bash
docker search mysql
```

Find the official image, and download it:

```bash
docker pull mysql
```

Now, you can run a MySQL container. Set up the necessary environment variables, such as MYSQL_ROOT_PASSWORD, and optionally link the container’s port to your host machine:

```bash
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql
```

This command creates a new container called some-mysql, sets the root password to my-secret-pw, and links port 3306 on the host to port 3306 on the container.

Example: PostgreSQL Image
For PostgreSQL, follow similar steps. First, search for the official image:

```bash
docker search postgres
```

Download the image:

```bash
docker pull postgres
```

Run a PostgreSQL container, making sure to key in necessary variables such as POSTGRES_PASSWORD:

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=my-secret-pw -p 5432:5432 -d postgres
```

Example: MongoDB Image
Running a MongoDB container follows the same steps. Search for the official image:

```bash
docker search mongo
```

Download the image:

```bash
docker pull mongo
```

Run a MongoDB container:

```bash
docker run --name some-mongo -p 27017:27017 -d mongo
```

## Testing with Docker

Docker lets you create separate, disposable environments that can be deleted when you’re done testing. This makes working with third party software, testing different pieces or versions, and experimenting swiftly all possible without risking your local setup.

Creating an Interactive Test Environment with Docker
To illustrate how to set up an interactive test environment, let’s use Python as an example. We will use a public Python image available on Docker Hub.

Start an interactive test environment using the Python image with this command:

```bash
docker run -it --rm python
```

This is a command ensuring you’re running the container interactively, and --rm flag will get rid of the container once it stops.

You should now be inside an interactive Python shell within the container. You can run any Python command or install more packages using pip as usual.

```python
print("Hello, Docker!")
```

Once you are done with your interactive session, you can type exit() or hit CTRL+D to quit the container. The container will be deleted as you've set the --rm flag.

Other Examples of Interactive Test Environments
There are many third-party images available on Docker Hub that you can use to create different interactive environments like:

Node.js: To start an interactive Node.js shell, run this command:

```bash
docker run -it --rm node
```

Ruby: To start an interactive Ruby shell, use this command:

```bash
docker run -it --rm ruby
```

MySQL: To start a temporary MySQL instance, use this command:

```bash
docker run -it --rm --name temp-mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -p 3306:3306 mysql
```

This command will start a temporary MySQL server accessible via host port 3306. After stopping, the instance will be gotten rid of.

Feel free to explore and test various software without worrying about messing up your local machine or installing unnecessary dependencies. Using Docker for interactive test environments helps you work more efficiently and cleanly when dealing with different third-party software.

## Command Line Utilities

Docker images can contain command line utilities or standalone applications that we can run inside containers. This can be very handy when working with third-party images, as the tools we want to use are already packaged and ready to be run without any installation or setup.

BusyBox

BusyBox is a small (1-2 Mb) and simple command line application that offers many common Unix utilities, such as awk, grep, vi, etc. To run BusyBox inside a Docker container, you just need to pull the image and run it with Docker:

```bash
docker pull busybox
docker run -it busybox /bin/sh
```

Once inside the container, you can begin running various BusyBox utilities like you would on a regular command line.

cURL

cURL is a popular command line tool that can be used to transfer data using various network protocols. It is commonly used for testing APIs or downloading files from the internet. To use cURL inside a Docker container, you can use the official cURL image available on Docker Hub:

```bash
docker pull curlimages/curl
docker run --rm curlimages/curl <https://example.com>
```

Here, the --rm flag is used to remove the container after the command finishes running. This is helpful when needing to run a single command then clean up the container afterwards.

Other Command Line Utilities

There are many command line utilities available in Docker images, including but not limited to:

wget: A free utility for non-interactive download of files from the Web.
imagemagick: A powerful software suite for image manipulation and conversion.
jq: A lightweight and flexible command-line JSON processor.
To use any of these tools, search for them on Docker Hub and follow the instructions given in their respective repositories.