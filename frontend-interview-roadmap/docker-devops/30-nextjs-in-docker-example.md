
# 30. Next.js in Docker Example

## Quick Revision

Dockerizing a **Next.js application** involves creating a `Dockerfile` that leverages multi-stage builds to produce an optimized production image. This image will contain the built Next.js application and a runtime environment (typically Node.js) to serve it, supporting SSR, SSG, and API Routes.

## Detailed Explanation

Next.js applications are unique because they can combine client-side rendering, server-side rendering, static site generation, and API routes. A Docker setup for Next.js needs to account for these different rendering strategies.

### Key Considerations

1.  **Multi-Stage Build:** Essential for keeping the production image small. One stage for building the Next.js app, and another for running it.
2.  **Base Image:** Use a Node.js base image (e.g., `node:18-alpine`) for both build and runtime stages.
3.  **Dependencies:** Install `npm` or `yarn` dependencies.
4.  **Build Process:** Run `next build` to compile the Next.js application.
5.  **Runtime:** The final image needs to run `next start` to serve the application, which handles SSR, SSG hydration, and API Routes.
6.  **Environment Variables:** Properly manage environment variables for different environments.
7.  **Non-Root User:** Run the application as a non-root user for security.

## Code Example

### Optimized Multi-Stage Dockerfile for a Next.js Application

```dockerfile
# Stage 1: Install dependencies
FROM node:18-alpine AS deps

WORKDIR /app

COPY package.json yarn.lock ./

RUN yarn install --frozen-lockfile

# Stage 2: Build the Next.js application
FROM node:18-alpine AS builder

WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules
COPY . .

ENV NEXT_TELEMETRY_DISABLED 1 # Disable Next.js telemetry during build

RUN yarn build

# Stage 3: Final production image
FROM node:18-alpine AS runner

WORKDIR /app

# Copy only necessary files from the builder stage
COPY --from=builder /app/next.config.js ./
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./

# Set environment variables for production
ENV NODE_ENV production
ENV PORT 3000 # Next.js listens on this port by default

# Create a non-root user for security
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
USER appuser

# Expose the port your Next.js app runs on
EXPOSE 3000

# Command to run the application
CMD ["yarn", "start"]
```

### `.dockerignore`

```
# .dockerignore
node_modules
.git
.env
.DS_Store
.next/cache
```

**To build and run this Dockerfile:**

1.  Save the above content as `Dockerfile` in your Next.js project root.
2.  Create a `.dockerignore` file as shown above.
3.  Build the image: `docker build -t my-nextjs-app .`
4.  Run the container: `docker run -p 3000:3000 my-nextjs-app`

Your Next.js application will be running inside a Docker container, accessible at `http://localhost:3000`.

## Resources

*   **Article:** [Next.js Docs - Docker Image](https://nextjs.org/docs/deployment/building-and-deploying/docker)
*   **Article:** [Dockerizing a Next.js Application](https://www.freecodecamp.org/news/dockerizing-a-next-js-application/)
*   **Video:** [Dockerizing Next.js Apps - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
