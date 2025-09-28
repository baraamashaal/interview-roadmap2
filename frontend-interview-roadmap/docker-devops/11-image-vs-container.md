
# 11. Docker Image vs. Container

## Quick Revision

In Docker, the terms **image** and **container** are fundamental but often confused. They are closely related but represent different stages in the Docker workflow.

*   **Docker Image:** A read-only, executable template that contains the application, its dependencies, libraries, and configuration. It's a blueprint for creating containers.

*   **Docker Container:** A runnable instance of a Docker image. It's a lightweight, isolated, and executable package that includes everything needed to run an application.

## Detailed Explanation

Think of it like object-oriented programming:

*   A **Docker Image** is like a **class**.
*   A **Docker Container** is like an **instance** of that class (an object).

### Docker Image

*   **Nature:** Read-only template.
*   **Creation:** Built from a `Dockerfile`.
*   **Contents:** Includes the application code, runtime, system tools, system libraries, and settings.
*   **Immutability:** Once an image is built, it doesn't change. If you need to make changes, you build a new image.
*   **Storage:** Stored in a Docker registry (e.g., Docker Hub) or locally on your machine.
*   **Purpose:** To provide a consistent and reproducible environment for your application.

### Docker Container

*   **Nature:** A runnable instance of an image.
*   **Creation:** Created from a Docker image using the `docker run` command.
*   **Contents:** Contains the image's layers plus a writable layer on top for any changes made during runtime.
*   **Lifecycle:** Can be started, stopped, moved, and deleted. Changes made to a running container are not persisted in the image unless explicitly committed.
*   **Isolation:** Isolated from other containers and the host system.
*   **Purpose:** To run your application in an isolated and consistent environment.

### Analogy

Consider a recipe for a cake:

*   The **recipe** is like a **Docker Image**. It contains all the instructions and ingredients needed to make the cake.
*   The **baked cake** is like a **Docker Container**. It's a runnable instance of the recipe. You can have multiple cakes (containers) from the same recipe (image).

## Code Examples

### Building an Image from a Dockerfile

```dockerfile
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

```bash
# Build the image
docker build -t my-node-app:1.0.0 .
# Here, 'my-node-app:1.0.0' is the name and tag of your Docker Image.
```

### Running a Container from an Image

```bash
# Run a container from the image
docker run -p 8080:3000 --name my-running-app my-node-app:1.0.0
# Here, 'my-running-app' is the name of your Docker Container.

# You can run multiple containers from the same image
docker run -p 8081:3000 --name my-second-app my-node-app:1.0.0
```

### Inspecting Images and Containers

```bash
# List all Docker images
docker images

# List all running Docker containers
docker ps

# List all Docker containers (including stopped ones)
docker ps -a
```

## Resources

*   **Article:** [Docker Docs - Get Started, Part 1: Orientation and setup](https://docs.docker.com/get-started/overview/)
*   **Article:** [Docker Image vs. Container: What's the Difference?](https://www.freecodecamp.org/news/docker-image-vs-container-whats-the-difference/)
*   **Video:** [Docker Images vs Containers Explained - TechWorld with Nana](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
