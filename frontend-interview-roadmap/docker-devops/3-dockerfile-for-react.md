
# 3. Dockerfile for React Applications

## Quick Revision

A **Dockerfile** is a text document that contains all the commands a user could call on the command line to assemble a Docker image. For a React application, a `Dockerfile` typically involves:

*   Using a Node.js base image.
*   Copying `package.json` and `yarn.lock` (or `package-lock.json`) to install dependencies.
*   Copying the application source code.
*   Building the React application for production.
*   Serving the static build assets, often with a lightweight web server like Nginx or by using a multi-stage build with a smaller base image.

## Detailed Explanation

Dockerizing a React application ensures that your application runs consistently across different environments, from development to production. A well-structured `Dockerfile` is key to creating efficient and secure Docker images.

### Multi-Stage Builds (Recommended)

Multi-stage builds are crucial for creating optimized Docker images for frontend applications. They allow you to:

1.  **Separate Build Environment:** Use a larger base image with all necessary build tools (Node.js, compilers) in a "builder" stage.
2.  **Create Production-Ready Image:** Copy only the essential build artifacts (the static `build` folder) to a much smaller, production-ready base image (e.g., Nginx or a minimal Node.js runtime) in a "runner" stage.

This significantly reduces the final image size, improving security and deployment speed.

### Key `Dockerfile` Instructions

*   **`FROM`:** Specifies the base image.
*   **`WORKDIR`:** Sets the working directory inside the container.
*   **`COPY`:** Copies files from the host to the container.
*   **`RUN`:** Executes commands during the image build process.
*   **`EXPOSE`:** Informs Docker that the container listens on the specified network ports at runtime.
*   **`CMD`:** Provides default commands for an executing container.

## Code Example

### Multi-Stage Dockerfile for a Create React App (CRA)

```dockerfile
# Stage 1: Build the React application
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package.json and yarn.lock (or package-lock.json)
COPY package.json yarn.lock ./

# Install dependencies
RUN yarn install --frozen-lockfile

# Copy the rest of the application code
COPY . .

# Build the React app for production
RUN yarn build

# Stage 2: Serve the static files with Nginx
FROM nginx:stable-alpine AS runner

# Copy the built React app from the builder stage to Nginx's public directory
COPY --from=builder /app/build /usr/share/nginx/html

# Copy custom Nginx configuration (optional)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80 (default for Nginx)
EXPOSE 80

# Command to start Nginx (default for nginx image)
CMD ["nginx", "-g", "daemon off;"]
```

**To build and run this Dockerfile:**

1.  Save the above content as `Dockerfile` in your React project root.
2.  Build the image: `docker build -t my-react-app .`
3.  Run the container: `docker run -p 80:80 my-react-app`

Your React application will be accessible at `http://localhost:80`.

## Resources

*   **Article:** [Docker Docs - Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
*   **Article:** [Docker Docs - Multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/)
*   **Article:** [Dockerizing a React App](https://www.freecodecamp.org/news/dockerizing-a-react-app/)
*   **Video:** [Docker for Frontend Developers - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
