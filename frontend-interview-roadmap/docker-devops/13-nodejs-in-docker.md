
# 13. Node.js in Docker

## Quick Revision

Running **Node.js applications in Docker containers** is a common and recommended practice. It provides a consistent, isolated, and portable environment for your Node.js app, ensuring it runs the same way everywhere. This involves creating a `Dockerfile` that specifies the Node.js runtime, installs dependencies, copies your application code, and defines how to start the application.

## Detailed Explanation

Dockerizing Node.js applications offers several advantages:

*   **Environment Consistency:** Avoids "it works on my machine" issues by packaging the exact Node.js version and dependencies.
*   **Dependency Management:** Isolates `node_modules` within the container, preventing conflicts with host system dependencies.
*   **Scalability:** Easily scale your Node.js services by running multiple containers.
*   **Portability:** Deploy your Node.js app to any cloud provider or server that supports Docker.
*   **Resource Isolation:** Containers can be configured with resource limits (CPU, memory).

### Key Considerations for Node.js Dockerfiles

1.  **Base Image:** Use official Node.js images (e.g., `node:18-alpine`, `node:lts`). Alpine variants are smaller and more secure.
2.  **`WORKDIR`:** Set a working directory inside the container (e.g., `/app`).
3.  **Dependency Installation:** Copy `package.json` and `yarn.lock` (or `package-lock.json`) first, then run `npm install` or `yarn install`. This leverages Docker's build cache efficiently.
4.  **Copy Application Code:** Copy the rest of your application code.
5.  **`EXPOSE`:** Document the port your Node.js application listens on.
6.  **`CMD`:** Define the command to start your application.
7.  **Non-Root User:** Run your application as a non-root user for security best practices.
8.  **Multi-Stage Builds:** Crucial for frontend Node.js apps (like Next.js or React) to keep the final image small by separating build-time dependencies from runtime dependencies.

## Code Example

### Optimized Dockerfile for a Node.js Backend Application

```dockerfile
# Stage 1: Build dependencies
FROM node:18-alpine AS deps
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# Stage 2: Build application (if applicable, e.g., TypeScript compilation)
# For a simple JS app, this stage might be merged with deps or skipped
FROM node:18-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
# If you have a build step (e.g., TypeScript), uncomment:
# RUN yarn build

# Stage 3: Final production image
FROM node:18-alpine AS runner

WORKDIR /app

# Copy only necessary files from builder stage
COPY --from=builder /app/package.json ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/. ./

# Set environment variables
ENV NODE_ENV production

# Create a non-root user for security
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
USER appuser

# Expose the port your Node.js app listens on
EXPOSE 5000

# Command to start the application
CMD ["node", "server.js"]
```

**To build and run this Dockerfile:**

1.  Save the above content as `Dockerfile` in your Node.js project root.
2.  Build the image: `docker build -t my-nodejs-app .`
3.  Run the container: `docker run -p 5000:5000 my-nodejs-app`

Your Node.js application will be accessible at `http://localhost:5000`.

## Resources

*   **Article:** [Docker Docs - Node.js best practices](https://docs.docker.com/language/nodejs/build-images/)
*   **Article:** [Optimizing Node.js Docker Images](https://www.freecodecamp.org/news/optimizing-node-js-docker-images/)
*   **Video:** [Dockerizing Node.js Apps - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
