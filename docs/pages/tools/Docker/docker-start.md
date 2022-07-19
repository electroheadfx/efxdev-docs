# Docker Start

## Find Docker Images

> Hub docker : https://hub.docker.com

# Basic

#### Docker image

```bash
docker image
```

**docker image essentials commands :**

```bash
docker image ...
 build # Build an image from a Dockerfile
 inspect # Display detailed information on one or more images
 load # Load an image from a tar archive or STDIN
 ls # List images
 prune # Remove unused images
 pull # Pull an image or a repository from a registry
 push # Push an image or a repository to a registry
 rm # Remove one or more images
 save # Save one or more images to a tar archive
 tag # Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
```

```bash
# shorcut for docker image ls
docker images
```

```bash
# delete an image
docker rmi image_name
```

#### Docker container

```bash
# list all container commands
docker container
# list all containers mounted
docker container ls
# list all containers (mounted and unmounted)
docker container ls -a
```

#### Docker pull

```bash
# Download an docker imagz with pull
docker pull hello-world
```

#### Docker run

```bash
# download image `ubuntu` and run in interactive mode like root user
# --rm delete the container when exit it
# bash is the command it run from the container
docker run -it --rm ubuntu bash
```

#### Docker activity with ps , rm, stop, prune

```bash
# list all containers running
docker ps
# list all containers running and stopped
docker ps -a
# stop a container
docker stop container_id
# delete a container
docker rm container_id
# CLEAN docker ram remove :
# - all stopped docker
# - all networks not used
# - all dangling images and build cache
docker system prune
```

## Practice with docker

```bash
# download image `debian` run and ssh login like root from it
# -it = execute in interactive mode for run command without exit
$ docker run -it debian
# --rm : Automatically remove the container when we exit bash window
$ docker run --rm -it debian    
# -v : Bind mount a volume
$ docker run --rm -it -v ${PWD}:/var/www/html debian        

# run a command from container
$ docker run -rm -it -v ${PWD}:/var/www/html \
    -p 8000:80 \ # Map 8O port from container to 8000 port
    php:apache \ # The image with apache like tag
    apache2-foreground # The command to run
```

> Docker run always mount a fresh container from image

## Docker creation (commit)

```bash
# List difference between the docker running and the image
$ docker diff container_id

# Save docker diff to the disk in a new image
$ docker commit container_id debiantest

# Exit and Export the new image
$ exit
$ docker save debiantest > /var/www/Lab/debiantest.tar
```

## Exemple `docker-wordpress`

> pas besoin de faire un `docker pull` 

```bash
# here we map the port of the container 80 to the machine 80
# -p external_port:container_port
$ docker run -p 80:80 tutum/wordpress
# with -d : run the container in background
```

> **WARMING** The date in container are not persisted, you lost all when you close the bash, so you need to sync the data to the disk :

```bash
# -v folder/to/your/disk:folder/in/docker
# --name is for name the container with a nice name : $ docker ps
# -d run docker in background task name ghost
$ docker run --name some-ghost -p 8080:2368 \
    -v /var/www/Lab/ghost:/varlib/ghost \
    -d ghost

# I modify file in /var/www/Lab/ghost
# if after I remove the container with:
$ docker rm -f some-ghost
# the container is destroyed
# if I re create the container with the image :
$ docker run --name some-ghost -p 8080:2368 \
    -v /var/www/Lab/ghost:/varlib/ghost \
    -d ghost
# The data is persisted because its always linked with /var/www/Lab/ghost
```

## Permission issue with Docker

> When you create file from container, the synchronized file are create like root user, it an issue. Just fix with `--user` param :

```bash
# ${PWD}:/app : app container mapped to current folder
$ docker run --rm -ti -v ${PWD}:/app --user 1000:100 -p 8000:80
# get the user
$ id -u
1000
# get group
$ id -g
100
# use it in docker run
$ docker run --rm -ti -v ${PWD}:/app --user $(id -u):$(id -g)
```