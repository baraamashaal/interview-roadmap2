
# 4. Multi-Stage Builds in Docker

## Quick Revision

**Multi-stage builds** are a powerful feature in Docker that allows you to create smaller, more efficient, and more secure Docker images. They work by using multiple `FROM` statements in a single `Dockerfile`, where each `FROM` instruction starts a new build stage. You can then selectively copy artifacts from one stage to another, leaving behind everything you don't need in the final image.

## Detailed Explanation

Without multi-stage builds, Dockerfiles for applications that require a build step (like frontend applications) often end up with large image sizes. This is because the final image contains all the build tools, development dependencies, and intermediate files that are only needed during the build process, not at runtime.

Multi-stage builds solve this problem by separating the build environment from the runtime environment.

### How Multi-Stage Builds Work

1.  **Build Stage:** The first stage (or stages) is used to build your application. It typically starts with a base image that includes all the necessary build tools and dependencies (e.g., `node:18-alpine` for a frontend app).
2.  **Copy Artifacts:** Once the application is built, you copy only the essential build artifacts (e.g., the `build` folder for a React app, or the `.next` folder for a Next.js app) to a new, much smaller base image.
3.  **Runtime Stage:** The final stage starts with a minimal base image (e.g., `nginx:stable-alpine` for serving static files, or a smaller `node:18-alpine` for a Node.js server) and only contains the runtime dependencies and the built application.

### Benefits of Multi-Stage Builds

*   **Smaller Image Sizes:** Significantly reduces the size of your final Docker image by excluding build tools and development dependencies.
*   **Improved Security:** Fewer components in the final image mean a smaller attack surface.
*   **Faster Deployment:** Smaller images are faster to pull and push.
*   **Cleaner Dockerfiles:** Separates concerns, making the `Dockerfile` easier to read and maintain.

## Code Example

### Multi-Stage Dockerfile for a Next.js Application

```dockerfile
# Stage 1: Install dependencies and build the application
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package.json and yarn.lock to install dependencies
COPY package.json yarn.lock ./

# Install dependencies
RUN yarn install --frozen-lockfile

# Copy the rest of your application code
COPY . .

# Build the Next.js application
RUN yarn build

# Stage 2: Create a smaller, optimized production image
FROM node:18-alpine AS runner

WORKDIR /app

# Set environment variables for production
ENV NODE_ENV production

# Copy necessary files from the builder stage
# Only copy what's needed for the Next.js production server
COPY --from=builder /app/next.config.js ./
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./

# Expose the port your Next.js app runs on
EXPOSE 3000

# Command to run the application
CMD ["yarn", "start"]
```

**Explanation:**

*   The first `FROM` statement defines the `builder` stage, where all dependencies are installed and the application is built.
*   The second `FROM` statement defines the `runner` stage, which starts with a fresh, minimal Node.js image.
*   The `COPY --from=builder` commands selectively copy only the output of the build process and necessary runtime files from the `builder` stage to the `runner` stage.

## Resources

*   **Article:** [Docker Docs - Multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/)
*   **Article:** [Reduce Docker Image Size with Multi-Stage Builds](https://www.freecodecamp.org/news/reduce-docker-image-size-with-multi-stage-builds/)
*   **Video:** [Docker Multi-Stage Builds Explained - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
