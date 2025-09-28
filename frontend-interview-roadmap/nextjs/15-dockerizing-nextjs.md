
# 15. Dockerizing Next.js Applications

## Quick Revision

**Dockerizing** a Next.js application involves packaging it into a Docker image, which can then be run as a container. This provides a consistent and isolated environment for your application, making deployment and scaling easier.

Key steps include:

*   Creating a `Dockerfile` to define the build process.
*   Using multi-stage builds for optimized image size.
*   Handling environment variables and dependencies.

## Detailed Explanation

Docker is a platform that uses OS-level virtualization to deliver software in packages called containers. Containers are isolated from each other and bundle their own software, libraries, and configuration files; they can communicate with each other through well-defined channels.

### Why Dockerize Next.js?

*   **Consistency:** Ensures your application runs the same way in development, staging, and production environments.
*   **Isolation:** Prevents conflicts between dependencies and environments.
*   **Scalability:** Easily scale your application by running multiple containers.
*   **Portability:** Deploy your application to any platform that supports Docker.

### `Dockerfile` Structure

A `Dockerfile` is a text document that contains all the commands a user could call on the command line to assemble an image.

**Common stages in a Next.js `Dockerfile`:**

1.  **Base Image:** Start with a Node.js base image.
2.  **Dependencies:** Install `npm` or `yarn` dependencies.
3.  **Build:** Build the Next.js application for production.
4.  **Production Image:** Create a smaller, optimized image for production, containing only the necessary files.

### Multi-Stage Builds

Multi-stage builds are a Docker feature that allows you to use multiple `FROM` statements in your `Dockerfile`. Each `FROM` instruction can use a different base image, and each `FROM` instruction begins a new stage of the build. You can selectively copy artifacts from one stage to another, leaving behind everything you don't need in the final image.

This is crucial for keeping your production Docker images small and secure.

## Code Example

```dockerfile
# Stage 1: Install dependencies and build the application
FROM node:18-alpine AS builder

WORKDIR /app

COPY package.json yarn.lock ./ 

RUN yarn install --frozen-lockfile

COPY . .

RUN yarn build

# Stage 2: Create a smaller, optimized production image
FROM node:18-alpine AS runner

WORKDIR /app

# Copy necessary files from the builder stage
COPY --from=builder /app/next.config.js ./
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./

# Set environment variables for production
ENV NODE_ENV production

# Expose the port your Next.js app runs on
EXPOSE 3000

# Command to run the application
CMD ["yarn", "start"]
```

### Building and Running the Docker Image

1.  **Build the image:**

    ```bash
docker build -t my-nextjs-app .
    ```

2.  **Run the container:**

    ```bash
docker run -p 3000:3000 my-nextjs-app
    ```

Now your Next.js application will be running inside a Docker container, accessible at `http://localhost:3000`.

## Resources

*   **Article:** [Next.js Docs - Docker Image](https://nextjs.org/docs/deployment/building-and-deploying/docker)
*   **Article:** [Dockerizing a Next.js Application](https://www.freecodecamp.org/news/dockerizing-a-next-js-application/)
*   **Video:** [Dockerizing Next.js Apps - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
