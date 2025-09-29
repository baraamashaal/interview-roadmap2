
# 16. Common Docker Commands

## Quick Revision

Mastering a few core Docker commands is essential for working with containers. These commands allow you to build images, run containers, manage their lifecycle, inspect their state, and clean up resources.

## Detailed Explanation

### 1. Image Management

*   **`docker build [OPTIONS] PATH | URL | -`:** Builds a Docker image from a `Dockerfile`.
    *   `docker build -t my-image:1.0 .` (builds from current directory, tags as `my-image:1.0`)
*   **`docker images [OPTIONS]`:** Lists all Docker images on your system.
    *   `docker images -a` (shows all images, including intermediate ones)
*   **`docker pull NAME[:TAG]`:** Pulls an image or a repository from a registry.
    *   `docker pull ubuntu:latest`
*   **`docker rmi [OPTIONS] IMAGE [IMAGE...]`:** Removes one or more images.
    *   `docker rmi my-image:1.0`
*   **`docker save [OPTIONS] IMAGE [IMAGE...]`:** Saves one or more images to a tar archive.
    *   `docker save -o my-image.tar my-image:1.0`
*   **`docker load [OPTIONS]`:** Loads an image from a tar archive.
    *   `docker load -i my-image.tar`

### 2. Container Management

*   **`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`:** Creates and starts a new container from an image.
    *   `docker run -p 80:80 -d --name my-web-app my-image` (run in detached mode, map port 80, name container)
*   **`docker ps [OPTIONS]`:** Lists running containers.
    *   `docker ps -a` (lists all containers, including stopped ones)
*   **`docker start [OPTIONS] CONTAINER [CONTAINER...]`:** Starts one or more stopped containers.
    *   `docker start my-web-app`
*   **`docker stop [OPTIONS] CONTAINER [CONTAINER...]`:** Stops one or more running containers.
    *   `docker stop my-web-app`
*   **`docker restart [OPTIONS] CONTAINER [CONTAINER...]`:** Restarts one or more containers.
    *   `docker restart my-web-app`
*   **`docker rm [OPTIONS] CONTAINER [CONTAINER...]`:** Removes one or more stopped containers.
    *   `docker rm my-web-app`
*   **`docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`:** Runs a command in a running container.
    *   `docker exec -it my-web-app bash` (opens an interactive bash shell in the container)
*   **`docker logs [OPTIONS] CONTAINER`:** Fetches the logs of a container.
    *   `docker logs -f my-web-app` (follows log output)

### 3. Volume Management

*   **`docker volume create [OPTIONS] VOLUME`:** Creates a new volume.
    *   `docker volume create my-data`
*   **`docker volume ls [OPTIONS]`:** Lists volumes.
*   **`docker volume rm [OPTIONS] VOLUME [VOLUME...]`:** Removes one or more volumes.

### 4. Network Management

*   **`docker network create [OPTIONS] NETWORK`:** Creates a new network.
*   **`docker network ls [OPTIONS]`:** Lists networks.
*   **`docker network rm [OPTIONS] NETWORK [NETWORK...]`:** Removes one or more networks.

### 5. System Commands

*   **`docker info`:** Displays system-wide information.
*   **`docker version`:** Shows the Docker version information.
*   **`docker system prune [OPTIONS]`:** Removes unused Docker data (stopped containers, dangling images, unused networks, build cache).
    *   `docker system prune -a` (removes all unused data, including build cache)

## Code Examples

```bash
# Build an image from a Dockerfile in the current directory
docker build -t my-frontend-app:latest .

# Run the frontend app, mapping host port 3000 to container port 80
docker run -p 3000:80 -d --name frontend-dev my-frontend-app:latest

# Check if the container is running
docker ps

# View logs of the frontend container
docker logs frontend-dev

# Stop the container
docker stop frontend-dev

# Remove the container
docker rm frontend-dev

# Remove the image
docker rmi my-frontend-app:latest

# Clean up all unused Docker resources
docker system prune -a
```

## Resources

*   **Official Docs:** [Docker CLI Reference](https://docs.docker.com/engine/reference/commandline/docker/)
*   **Cheat Sheet:** [Docker Cheat Sheet](https://www.docker.com/sites/default/files/d8/2019-09/docker-cheat-sheet.pdf)
*   **Video:** [Docker Commands Crash Course - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
