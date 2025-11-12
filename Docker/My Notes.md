### Download Image

It will download a docker image locally from docker hub.

```bash
docker pull image_name
```

### View Images

```bash
docker images
```

Second approach

```bash
docker image ls
```

### Run an Image

```bash
docker run image_name
```

**Note:** with that command docker builds a container and immediately exits. Because container has nothing to do, if you want to run a container in the background for infinite amount of time you can run

```bash
docker run image_name sleep infinite 
```

**Note:** jab yeah command run hogi to terminal stuck ho jaye ga, tum koee command nahi likh saktey, is ka solution aglay section mey dehktay heyn.

**--detach**

The detach option will run the container in the background and give your terminal control back, you can run the next command, the short hand for detach is `-d`

```bash
docker run -d image_name sleep infinite
```

## Naming a Container

When running a new container from an image you can give the container a name so that you don't have to check for id of the container again and again.

```bash
docker run -it --name asif image_name
```

### Remove Image

```bash
docker image rm image_name
```

**Note:** if a container is using an image you cannot remove it.

#### Remove all Images

```bash
docker image prune
```

**Note:** This will only remove dangling images. When you build a new image with the same tag as an old one, the old image loses its tag and becomes "dangling." For example:

```bash
docker build -t my-app:latest .
# Build again with same tag
docker build -t my-app:latest .
```

If you wondering what's this build command do, it's build an image from a `Dockerfile` basically it's a file that contains configuration to build a docker image, and -t saying that the next argument is gonna be a tag with name, the tag is version.

## Container

### List Containers

This command will list down all running/active containers

```bash
docker ps
```

To view all containers including inactive one, you can run

```bash
docker ps -a
```

There are also many aliases for ps command, you can take a look, for example

```bash
docker containers list --all
```

You make this commmand even shorter

```bash
docker container ls -a
```

### Run Container

```bash
docker start conatiner_name/id
```

It will exit as the main process will completed inside container.

### Remove Container

```bash
docker container rm container_name/id
```

Second approach

```bash
docker rm container_name/id
```

#### Kill a Container

```bash
docker container kill container_name
```

Second apporach

```bash
docker kill container_name/id
```

#### Run Command inside Container

To run a command inside container without entering into the container you can use 

```bash
docker run -it ubuntu ls
```

It will starts the container and list down all files and exits

#### Remove all Containers

```bash
docker container prune
```

This will remove all stoped containers.

### Connect Terminal with Container

```bash
docker exec -it containername sh
```

It will let you run commands in container's terminal

### Port Maping

```bash
docker run -it -p host_port:contianer_port image
```

You can aslo part multiple ports;

```bash
... -p host:container -p host:container image
```

#### Auto Port Mapping

Manually mapping a bunch of different ports is pretty hectic, let say you have a lot of different ports and you automatically want them to be exposed by the docker. 

In that case you can use auto port mapping, and docker will map a randomly available port of the host on the exposed port by container.

**Dockerfile**

```bash
EXPOSE 3000 4000 5000
```

And now whenever you spin up a new container after building image from Dockerfile, you have to mention the `P` flag, its a capital P.

```bash
docker run -it -P --name my-app image_name
```

## Remove Container on Stop

The `--rm` flag automatically removes a container when it stops/exits. It's a cleanup feature that helps keep your system tidy!

```bash
docker run --rm <image>
```

When you use `--rm`, container is automatically deleted when it stops then it will Cleans up disk space automatically and removes anonymous volumes associated with the container

**Note:** Container cannot be restarted after it exits

## How to push an image on docker?

First tag the image, there are two ways to tag an image either after build:

```bash
docker tag imagename username/imagename:latest  
```

Or you can tag while builiding the image

```bash
docker build -t username/imagename path_to_docker_file
```

Once the image is tag just run:-

```bash
docker push imagename
```

**Note:** Before pushing the image make sure you are login:_

```bash
docker login
```

## Overiding Env

Ager apney docker file k ander koee enviornment variable create kiya hey using:-

```bash
ENV PORT=3000 # inside docker file
```

Now ager app PORT env ko ager overide karna chahtey hey to ap `-e` flag use kar saktey hey.

```bash
docker run -e PORT=2000 image_name 
```

## Passing .env File

```bash
docker run --env-file ./.evn image_name
```

# 
