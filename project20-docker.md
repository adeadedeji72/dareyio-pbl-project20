# MIGRATION TO THE СLOUD WITH CONTAINERIZATION. PART 1 – DOCKER AND DOCKER COMPOSE #

## Install Docker and prepare for migration to the Cloud ##
**Install from a Package**

Go to https://download.docker.com/linux/ubuntu/dists/, choose your Ubuntu version, then browse to pool/stable/, choose amd64, armhf, arm64, or s390x, and download the .deb file for the Docker Engine version you want to install.

Install Docker Engine, changing the path below to the path where you downloaded the Docker package.
~~~
 sudo dpkg -i /path/to/package.deb
~~~

The Docker daemon starts automatically.

Verify that Docker Engine is installed correctly by running the hello-world image.
~~~
 sudo docker run hello-world
~~~
This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

** Manage Docker as non-root user
The Docker daemon binds to a Unix socket instead of a TCP port. By default that Unix socket is owned by the user root and other users can only access it using sudo. 
The Docker daemon always runs as the root user.

If you don’t want to preface the docker command with sudo, create a Unix group called docker and add users to it. When the Docker daemon starts, 
it creates a Unix socket accessible by members of the docker group.

To create the docker group and add your user:

Create the docker group.
~~~
 sudo groupadd docker
~~~
Add your user to the docker group.
~~~
 sudo usermod -aG docker $USER
~~~
Log out and log back in so that your group membership is re-evaluated.

If testing on a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.

On a desktop Linux environment such as X Windows, log out of your session completely and then log back in.

On Linux, you can also run the following command to activate the changes to groups:
~~~
 newgrp docker 
~~~
Verify that you can run docker commands without sudo.

~~~
docker run hello-world
~~~

### **MySQL in container** ###

Let us start assembling our application from the Database layer – we will use a pre-built MySQL database container, configure it, and make sure it is ready to receive requests from our PHP application.

**Step 1: Pull MySQL Docker Image from Docker Hub Registry**
Start by pulling the appropriate Docker image for MySQL. You can download a specific version or opt for the latest release, as seen in the following command:
~~~
docker pull mysql/mysql-server:latest
~~~
List the images with
~~~
docker image ls
~~~
![](docker_image_ls.jpg)
