# Port Mapping in Docker

Port mapping is a networking feature that allows you to connect ports on your host machine to ports inside a Docker container. It acts as a bridge between the outside world and your containerized application.

## How It Works

When you run a container, services inside it listen on specific ports (like port 8080 for a web server). However, by default, these ports aren't accessible from your host machine or the network. Port mapping solves this by forwarding traffic from a host port to a container port.

For example, you might map host port 3000 to container port 8080:

- Requests to `localhost:3000` on your machine get forwarded to port 8080 inside the container
- The container's application receives the request and responds

## Basic Syntax

The most common way to set up port mapping is with the `-p` flag:

```bash
docker run -p 3000:8080 my-app
```

This maps host port 3000 to container port 8080. You can also specify the IP address:

```bash
docker run -p 127.0.0.1:3000:8080 my-app
```
