# Docker intro & fundamentals

## Key Concepts

- **Containers** are packaged applications containing everything they need to run in an isolated environment. This isolation allows them to run consistently across different environments.
- **Images** are immutable templates (snapshots) of an application, while a **container** is a running instance of an image.
- **Docker Engine** is the runtime responsible for building images and running, managing, and stopping containers.
- A **Dockerfile** contains instructions that Docker executes top to bottom to build an image. Each instruction creates a layer, and each layer depends on the filesystem state of the previous layer.
- **Layer caching** allows Docker to reuse unchanged layers, making builds faster. If a layer changes, all subsequent layers must be rebuilt, which is why Dockerfile order matters.
- A **hypervisor** is software that allows a physical machine to run multiple full operating systems at the same time.
- **Containers share the host OS kernel**, making them faster and more lightweight than **virtual machines**, which run a full guest operating system.

## Commands

- `docker build -t <image-name> .` – Builds an image using the Dockerfile in the current directory
- `docker run <image-name>` – Creates and runs a container from an image
- `docker images` – Lists all Docker images stored locally
- `docker ps` – Lists running containers
- `docker ps -a` – Lists all containers, including stopped ones

## Examples

### Basic Dockerfile
```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY app.py .
CMD ["python", "app.py"]
```

## What I Learned

I learned that Docker is not just a tool but a system for building predictable and repeatable environments. Images are immutable templates, and containers are running instances created from them. Docker builds images layer by layer from top to bottom, and caching depends on whether layers and their build context change. This means Dockerfile order directly affects build speed, CI/CD performance, and even cloud cost. Containers are lightweight because they share the host operating system kernel, which is why they start faster and scale better than virtual machines.
