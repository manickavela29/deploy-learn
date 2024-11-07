# Docker

1. Docker is a containerisation platform – it is a toolkit that allows you to build, deploy and manage containerised applications.
2. Docker separates applications from infrastructure so that software can be delivered quickly.
3. Infrastructure is managed in the same way as application. DevOps came into existence
4. Docker's methodologies for shipping, testing, and deploying code, significantly reduced the delay between writing code and running it in production.

## Docker Architectures

1. Docker uses Client-Server architecture
2. Docker client talks to Docker Daemon, heavy lifting of building, running, and distributing your Docker containers.
3. client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon.
    - Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface

![docker architecture](imgs/docker-architecture.webp)

## docker Terminologies

1. Docker Daemon (dockerd): 
    - listens to API requests
    - manages Docker objects [images, containers, networks, volumes]
    - communicates with other system Daemons

2. Docker Client (docker):
    - primary docker user interaction
    - docker cmd uses docker API
    - docker run , client sends cmd to dockerd

3. Docker registory
    - Stores docker images
    - Docker hub - public regeistory
    - cmds : docker push, docker pull, or docker run

Docker objects

4. Images:
    - readonly template with instruction to create Docker containers
    - often images are based on another image
    - Dockerfile is used to build images, with users defining the steps

5. Containers :
    - Runnable instances of an image
    - create, start, stop, move, delete using docker cli
    - connect to networks, attach to storage or create new image from current state

6. buildx :
    - building docker image for different devices and architectures
    - linux/arm64, linux/amd64

## Image types 

1. Base Images & Child Images
2. Official images & User Images
    - NGC containers : https://catalog.ngc.nvidia.com/containers
    - user/image-name

## The Dockerfile

- FROM     - Specifies base image
- WORKDIR  - sets current working dir, subsequent cmds inside dir
- COPY     - Copies files from source to dir,
- CMD      - cmd instruction, specifies what to run when created

# Regular docker cmds

## image

```bash
# Bulding and tagging
docker build -t <image_name>:<tag> <path>
docker tag <source_image> <target_image>
docker tag <image_name>:<old_tag> <image_name>:<new_tag>


# Pulling and pushing image
docker pull <image_name>:<tag>
docker push <image_name>:<tag>

# Listing and Inspecting the image
docker images
docker image inspect <image_name>:<tag>
docker image ls <image_name>

# Removing and cleaning up
docker rmi <image_name>:<tag>
docker image prune                  # Removes unused images(dangling images) not used by any container
docker image prune -a               # Removes all the images

# History and layer management
docker history <image_name>:<tag>
docker save -o <path>.tar <image_name>:<tag>
docker load -i <path>.tar

# Export and Import
docker export <container_id> > <path>.tar
docker import <path>.tar <new_image_name>:<tag>

# Running containers from images
docker run <image_name>:<tag>
docker run --rm <image_name>:<tag>                      # remove immediately after stopping
docker run -it <image_name>:<tag> bash

# listing images
docker image ls 

# Buildx based cmd
docker buildx build --platform <platform> -t <image_name>:<tag> <path>
docker builder prune                                    # Cleanes up buildx caches
```

## Docker container cmds in detail

```bash
# Running Containers
docker run <image_name>
docker run -d <image_name>
docker run --name <container_name> <image_name>
docker run -it <image_name> bash

# Starting and Stopping Containers
docker start <container_name>
docker stop <container_name>
docker restart <container_name>
docker kill <container_name>

# Listing Containers
docker ps: Lists all running containers.
docker ps -a: Lists all containers, including stopped ones.
docker ps -q: Lists only container IDs of running containers.

# Inspecting and Logging Containers
docker logs <container_name>: Displays the logs of a running or stopped container.
docker logs -f <container_name>: Follows live log output (useful for monitoring).
docker inspect <container_name>: Displays detailed information about a container (e.g., environment variables, volumes).
docker stats <container_name>: Shows live resource usage statistics for a container.

# Managing and Removing Containers
docker rm <container_name>: Removes a stopped container.
docker rm -f <container_name>: Forcefully removes a running container.
docker container prune: Removes all stopped containers, helping clean up disk space.

# Copying Files and Data
docker cp <container_name>:/path/in/container /path/on/host: Copies files from a container to the host.
docker cp /path/on/host <container_name>:/path/in/container: Copies files from the host to the container.

# Networking and Port Forwarding
docker run -p <host_port>:<container_port> <image_name>: Maps a container’s port to a port on the host.
docker network ls: Lists all Docker networks.
docker network inspect <network_name>: Shows details about a specific network.

# Attaching and Interacting with Containers
docker attach <container_name>: Attaches to a running container (useful for interactive mode).
docker exec -it <container_name> /bin/bash: Opens a shell session in a running container.
docker exec <container_name> <command>: Runs a command in a running container.

# Checking Health and Status
docker container ls --filter "status=exited": Lists only containers that have exited.
docker inspect -f '{{.State.Status}}' <container_name>: Checks the status of a specific container (running, stopped, etc.).

```

References
----------
1. https://docs.docker.com/get-started/docker-overview/