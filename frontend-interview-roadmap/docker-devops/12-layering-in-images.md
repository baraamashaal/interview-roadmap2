# 12. Layering in Docker Images

## Quick Revision

**Docker images** are built up from a series of read-only layers. Each instruction in a `Dockerfile` (e.g., `FROM`, `RUN`, `COPY`, `ADD`) creates a new layer. These layers are stacked on top of each other, forming the final image. When a container is run from an image, a new writable layer is added on top of the image layers.

## Detailed Explanation

Understanding image layering is fundamental to optimizing Docker image size, build speed, and security.

### How Layers Work

1.  **Read-Only Layers:** Each instruction in a `Dockerfile` creates a new read-only layer. These layers are cached by Docker.
2.  **Layer Caching:** If an instruction and its context haven't changed, Docker can reuse the cached layer, speeding up subsequent builds.
3.  **Union File System:** Docker uses a Union File System (UFS) to combine these layers. When you access a file in a container, UFS presents a unified view of all layers.
4.  **Writable Layer:** When a container is started, a new writable layer is added on top of the read-only image layers. Any changes made to the container (e.g., creating files, modifying data) are written to this writable layer.

### Benefits of Layering

*   **Efficiency:** Layers are shared between images. If multiple images use the same base image, they only need to store the base image layers once.
*   **Caching:** Speeds up builds by reusing cached layers.
*   **Version Control:** Each layer can be thought of as a version of the image.
*   **Security:** Changes to the writable layer do not affect the underlying image layers.

### Impact on Image Size and Build Speed

*   **Order of Instructions:** Place instructions that change less frequently at the top of your `Dockerfile` to maximize cache hits.
*   **Combine `RUN` Commands:** Group multiple `RUN` commands using `&&` to reduce the number of layers and potentially improve caching.
*   **Multi-Stage Builds:** This is the most effective way to leverage layering. It allows you to discard intermediate layers (containing build tools and development dependencies) from the final production image, resulting in much smaller images. (See question 4 for more details).

## Code Example

### `Dockerfile` Demonstrating Layers

```dockerfile
# Layer 1: Base image
FROM ubuntu:20.04

# Layer 2: Install dependencies (often changes less frequently than app code)
RUN apt-get update && apt-get install -y \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Layer 3: Create working directory
WORKDIR /app

# Layer 4: Copy package.json and install node modules
# This layer is invalidated if package.json or yarn.lock changes
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# Layer 5: Copy application code
# This layer is invalidated if any application code changes
COPY . .

# Layer 6: Build the application
RUN yarn build

# Layer 7: Expose port
EXPOSE 3000

# Layer 8: Command to run the application
CMD ["yarn", "start"]
```

**Explanation:**

*   Each `FROM`, `RUN`, `COPY`, `ADD` instruction creates a new layer.
*   When you rebuild the image, Docker will try to reuse layers from its cache. If, for example, only your application code changes (Layer 5), Docker will reuse Layers 1-4 and only rebuild Layers 5-8.

## Resources

*   **Article:** [Docker Docs - Understand images, containers, and storage drivers](https://docs.docker.com/storage/storagedriver/)
*   **Article:** [Docker Docs - Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
*   **Video:** [Docker Image Layers Explained - TechWorld with Nana](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
