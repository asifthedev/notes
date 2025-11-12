# Docker

It's a virtualization tool that helps you create isolated containers that package your application's source code along with all its dependencies and enviornment variables required to run it. 

This approach enables scalability and resolves environment conflicts when running your application across different machines.

It provide consistency accross environments and ensures our application run the same on my computer and your computer.

**No more:** "it works on my machine 😂"

## Virtualization

Virtualization is the process of creating virtual versions of physical computing resources, like servers, storage, CPU, or networks, using software. 

## Virtual Machine

A virtual machine is an isolated Operating System running in a software defined or emulated enviornment, it has virtual resources like CPU, storage, and RAM etc. 

## Containerization vs Virtulization

**Virtual Machine:** Each VM runs its own complete operating system, which takes a lot of memory and storage. When you scale up, spinning up a new VM takes minutes to boot and consumes lots of resources. This is wasteful and slow.

**Docker Container:** Docker doesn't need a separate OS. It runs on top of the host OS kernel and packages only your application and dependencies. Containers are lightweight (few MB), start in seconds, and you can run thousands on one machine. This makes scaling fast and cost-effective.

**In short:** VMs are heavy and slow to scale. Docker is lightweight and scales quickly.

<img title="" src="https://media.licdn.com/dms/image/v2/D4E12AQGgYr1rG_0dQQ/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1663509874484?e=2147483647&v=beta&t=cpRYmxIuvN_qoEGN-DZQTT5ifnmxvCRWZX9HvOcSy6w" alt="Containerization VS Virtualization" width="366" data-align="center">

## Docker Architecture

### Client

Client woh interface jo ham use kartey hey docker k sath interact karney kelye woh do tarah say hota ya to ap docker desktop app ki help say kar saktey ho ya phir terminal k througe, yahi docker client hey.

### Host

**Docker Host** is the machine (computer or server) where Docker is installed and running. 

### Docker Daemon

**Docker Daemon** is the background service that runs on your Docker Host and manages all Docker operations.

**Manages Containers:** Creates, starts, stops, and deletes containers

**Manages Images:** Handles Docker images, pulls them from registries, and stores them locally

**Manages Networks:** Sets up networking between containers

**Manages Storage:** Handles volumes and data persistence

**Listens to Commands:** Receives commands from the Docker Client and executes them

## Docker Image

- A **blueprint** or **template** for creating containers
- Contains your application code, dependencies, libraries, and everything needed to run the app
- It's **static** (doesn't change) and **read-only**
- Stored on disk
- Think of it like a **class in programming** 

## Docker Container

- A **running instance** of a Docker image
- When you run an image, it becomes a container
- It's **dynamic** (changes as it runs) and can read/write data
- Think of it like an **object created from a class**


