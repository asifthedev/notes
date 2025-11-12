# Docker

### Build an image from a Dockerfile

Creates a Docker image from a Dockerfile with a specified name and path.

```bash
docker build -t image_name path_to_dockerfile
```

**-t**

Tag (assigns a name and optional tag to the image)

### List all local images

Displays all Docker images stored locally on the system.

```bash
docker images
docker image ls
```

### Pull an image from Docker Hub

Downloads a specific image from Docker Hub repository.

```bash
docker pull image_name:tag
```

### Remove a local image

Deletes a Docker image from the local system.

```bash
docker rmi image_name:tag
docker rm [image_name/image_id]
```

**rmi**

Short of remove image 

**rm**

Short hand of remove

### Tag an image

Assigns a new tag/name to an existing Docker image.

```bash
docker tag source_image:tag new_image:tag
```

### Push an image to Docker Hub

Uploads a Docker image to Docker Hub repository.

```bash
docker push image_name:tag
```

### Inspect details of an image

Shows detailed information about a specific Docker image.

```bash
docker image inspect image_name:tag
```

### Save an image to a tar archive

Exports a Docker image to a tar file for backup or transfer.

```bash
docker save -o image_name.tar image_name:tag
```

**Flags:** `-o` = output (specifies the output tar file path)

### Load an image from a tar archive

Imports a Docker image from a tar file.

```bash
docker load -i image_name.tar
```

**Flags:** `-i` = input (specifies the input tar file path)

### Prune unused images

Removes all dangling and unused Docker images to free up space.

```bash
docker image prune
```

## Docker Containers

### Run a container from an image

Starts a new container from a specified image.

```bash
docker run container_name image_name
```

### Run a named container from an image

Starts a new container with a specific name from an image.

```bash
docker run --name container_name image_name:tag
```

**Flags:** `--name` = assigns a custom name to the container

### List all running containers

Shows all currently active and running containers, `ps` stands for process status.

```bash
docker ps
```

### List all containers (including stopped ones)

Displays all containers, both running and stopped.

```bash
docker ps -a
```

**Flags:** `-a` = all (shows all containers including stopped ones)

### Stop a running container

Gracefully stops a running container.

```bash
docker stop container_name_or_id
```

### Start a stopped container

Restarts a previously stopped container.

```bash
docker start container_name_or_id
```

### Run container in interactive mode

Starts a container and allows interaction through terminal input/output.

```bash
docker run -it container_name_or_id
```

**Flags:** `-i` = interactive (keeps STDIN open) | `-t` = tty (allocates a pseudo-terminal)

### Run container in interactive shell mode

Starts a container with an interactive shell session.

```bash
docker run -it container_name_or_id sh
```

**Flags:** `-i` = interactive | `-t` = tty | `sh` = shell command to execute

### Remove a stopped container

Deletes a stopped container from the system.

```bash
docker rm container_name_or_id
```

### Remove a running container (forcefully)

Forcibly stops and removes a running container.

```bash
docker rm -f container_name_or_id
```

**Flags:** `-f` = force (forcefully removes running container without stopping)

### Inspect details of a container

Displays detailed information about a specific container.

```bash
docker inspect container_name_or_id
```

### View container logs

Shows the output and error logs from a container.

```bash
docker logs container_name_or_id
```

### Pause a running container

Temporarily suspends a running container without stopping it.

```bash
docker pause container_name_or_id
```

### Unpause a paused container

Resumes a previously paused container.

```bash
docker unpause container_name_or_id
```

---

## Docker Volumes

### Create a named volume

Creates a named volume for persistent data storage.

```bash
docker volume create volume_name
```

### List all volumes

Displays all Docker volumes on the system.

```bash
docker volume ls
```

### Inspect details of a volume

Shows detailed information about a specific volume.

```bash
docker volume inspect volume_name
```

### Remove a volume

Deletes a Docker volume from the system.

```bash
docker volume rm volume_name
```

### Run a container with a volume (mount)

Starts a container and mounts a volume to a specified path.

```bash
docker run --name container_name -v volume_name:/path/in/ image_name:tag
```

**Flags:** `--name` = assigns a custom name to the container | `-v` = volume (mounts a volume to the specified path)

### Copy files between a container and a volume

Transfers files from local system to a container's mounted volume.

```bash
docker cp local_file_or_directory container_name:/path/in/
```

---

## Docker Networks

### Run a container with port mapping

Starts a container and maps host ports to container ports.

```bash
docker run --name container_name -p host_port:container_port image_name
```

**Flags:** `--name` = assigns a custom name to the container | `-p` = port (maps host port to container port)

### List all networks

Displays all Docker networks available on the system.

```bash
docker network ls
```

### Inspect details of a network

Shows detailed information about a specific Docker network.

```bash
docker network inspect network_name
```

### Create a user-defined bridge network

Creates a custom bridge network for container communication.

```bash
docker network create network_name
```

### Connect a container to a network

Attaches a running container to a specific network.

```bash
docker network connect network_name container_name
```

### Disconnect a container from a network

Removes a container from a specific network.

```bash
docker network disconnect network_name container_name
```

---

## Docker Compose

### Create and start containers defined in a docker-compose.yml file

Starts all services defined in the docker-compose.yml file in the background.

```bash
docker compose up
```

### Stop and remove containers defined in a docker-compose.yml file

Stops and removes all containers, networks, and volumes defined in docker-compose.yml.

```bash
docker compose down
```

### Build or rebuild services

Builds or rebuilds Docker images for all services in docker-compose.yml.

```bash
docker compose build
```

### List containers for a specific Docker Compose project

Shows all running containers for the services defined in docker-compose.yml.

```bash
docker compose ps
```

### View logs for services

Displays logs from all services defined in docker-compose.yml.

```bash
docker compose logs
```

### Scale services to a specific number of containers

Runs multiple instances of a service specified in docker-compose.yml.

```bash
docker compose up -d --scale service_name=number_of_containers
```

**-d**

Detach (runs services in background) 

**--scale**

Scales the number of containers for a service

### Run a one-time command in a service

Executes a single command in a service container without starting all services.

```bash
docker compose run service_name command
```

### List all volumes

Displays all volumes created for Docker Compose services.

```bash
docker volume ls
```

### Pause a service

Temporarily suspends a service without stopping it.

```bash
docker compose pause service_name
```

### Unpause a service

Resumes a previously paused service.

```bash
docker compose unpause service_name
```

### View details of a service

Displays detailed information about a specific service.

```bash
docker compose ps service_name
```

# 

## Latest Docker

### Initialize Docker inside an application

```
docker init
```

### Watch the service/container of an application

```
docker compose watch
```

It watches build context for service and rebuild/refresh containers when files are updated.

---

## Dockerfile Reference

### What is a Dockerfile?

A Dockerfile is a script that contains instructions for building a Docker image. It defines the base image, sets up environment variables, installs software, and configures the container for a specific application or service.

### Dockerfile Syntax

#### FROM

Specifies the base image for the Docker image.

```
FROM image_name:tag

# Example
FROM ubuntu:20.04
```

#### WORKDIR

Sets the working directory for subsequent instructions.

```
WORKDIR /path/to/directory

# Example
WORKDIR /app
```

#### COPY

Copies files or directories from the build context to the container.

```
COPY host_source_path container_destination_path

# Example
COPY . .
```

#### RUN

Executes commands in the shell.

```
RUN command1 && command2

# Example
RUN apt-get update && apt-get install -y curl
```

#### ENV

Sets environment variables in the image.

```
ENV KEY=VALUE

# Example
ENV NODE_VERSION=14
```

#### EXPOSE

Informs Docker that the container listens on specified network ports at runtime.

```
EXPOSE port

# Example
EXPOSE 8080
```

#### CMD

Provides default commands or parameters for an executing container.

```
CMD ["executable","param1","param2"]

# Example
CMD ["npm", "start"]
```

Or:

```
CMD executable param1 param2

# Example
CMD npm run dev
```

#### ENTRYPOINT

Configures a container that will run as an executable.

```
ENTRYPOINT ["executable","param1","param2"]

# Example
ENTRYPOINT ["node", "app.js"]
```

Or:

```
ENTRYPOINT executable param1 param2

# Example
ENTRYPOINT node app.js
```

#### ARG

Defines variables that users can pass at build-time to the builder with the docker build command.

```
ARG VARIABLE_NAME=default_value

# Example
ARG VERSION=latest
```

#### VOLUME

Creates a mount point for external volumes or other containers.

```
VOLUME /path/to/volume

# Example
VOLUME /data
```

#### LABEL

Adds metadata to an image in the form of key-value pairs.

```
LABEL key="value"

# Example
LABEL version="1.0" maintainer="Adrian"
```

#### USER

Specifies the username or UID to use when running the image.

```
USER user_name

# Example
USER app
```

#### ADD

Copies files or directories and can extract tarballs in the process.

```
ADD source_path destination_path

# Example
ADD ./app.tar.gz /app
```

Similar to COPY, but with additional capabilities (e.g., extracting archives).

### Dockerfile Example

```dockerfile
# Use an official Node.js runtime as a base image
FROM node:20-alpine

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the current directory contents to the container at /app
COPY . .

# Expose port 8080 to the outside world
EXPOSE 8080

# Define environment variable
ENV NODE_ENV=production

# Run app.js when the container launches
CMD node app.js
```

## Docker Compose File Reference

### What is a Docker Compose File?

A Docker Compose file is a YAML file that defines a multi-container Docker application. It specifies the services, networks, and volumes for the application, along with any additional configuration options.

### Docker Compose File Syntax

#### version

Specifies the version of the Docker Compose file format.

```yaml
version: '3.8'
```

#### services

Defines the services/containers that make up the application.

```yaml
services:
  web:
    image: nginx:latest
```

#### networks

Configures custom networks for the application.

```yaml
networks:
  my_network:
    driver: bridge
```

#### volumes

Defines named volumes that the services can use.

```yaml
volumes:
  my_volume:
```

#### environment

Sets environment variables for a service.

```yaml
environment:
  - NODE_ENV=production
```

#### ports

Maps host ports to container ports.

```yaml
ports:
  - "8080:80"
```

#### depends_on

Specifies dependencies between services, ensuring one service starts before another.

```yaml
depends_on:
  - db
```

#### build

Configures the build context and Dockerfile for a service.

```yaml
build:
  context: .
  dockerfile: Dockerfile.dev
```

#### volumes_from

Mounts volumes from another service or container.

```yaml
volumes_from:
  - service_name
```

#### command

Overrides the default command specified in the Docker image.

```yaml
command: ["npm", "start"]
```

### Docker Compose File Example

Here's a simple Docker Compose file example for a MERN stack with web and database service:

```yaml
version: '3.8'

# Define services for the MERN stack
services:
  # MongoDB service
  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - /data/db
      - mongo_data
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: admin

  # Node.js (Express) API service
  api:
    # Specify the build context for the API service
    build:
      context: ./api
      # Specify the Dockerfile for building the API service
      dockerfile: Dockerfile
    ports:
      - "5000:5000"
    # Ensure the MongoDB service is running before starting the API
    depends_on:
      - mongo
    environment:
      MONGO_URI: mongodb://admin:admin@mongo:27017/mydatabase
    networks:
      - mern_network

  # React client service
  client:
    build:
      # Specify the build context for the client service
      context: ./client
      # Specify the Dockerfile for building the client service
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    # Ensure the API service is running before starting the client
    depends_on:
      - api
    networks:
      - mern_network

# Define named volumes for persistent data
volumes:
  mongo_data:

# Define a custom network for communication between services
networks:
  mern_network:
```
