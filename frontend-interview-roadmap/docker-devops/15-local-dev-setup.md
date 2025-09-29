
# 15. Local Development Setup with Docker

## Quick Revision

Using Docker for your **local development setup** provides a consistent, isolated, and reproducible environment that mirrors your production setup. This eliminates "it works on my machine" issues and streamlines onboarding for new developers. Key aspects include:

*   **Docker Compose:** To orchestrate multiple services (frontend, backend, database).
*   **Bind Mounts:** To synchronize local code changes with containers for hot-reloading.
*   **Environment Variables:** To configure development-specific settings.
*   **Port Mapping:** To access services from your host browser.

## Detailed Explanation

Setting up a local development environment can often be complex, involving installing specific versions of Node.js, databases, and other services. Docker simplifies this by encapsulating all these dependencies within containers.

### Benefits for Local Development

*   **Consistency:** Ensures all developers work in the same environment, reducing configuration drift.
*   **Isolation:** Prevents conflicts between different projects or global dependencies on your host machine.
*   **Easy Onboarding:** New team members can get up and running quickly with a single `docker-compose up` command.
*   **Production Parity:** Develop in an environment that closely resembles production, reducing deployment surprises.
*   **Version Control:** Your `Dockerfile` and `docker-compose.yml` are version-controlled, making environment changes trackable.

### Key Docker Features for Local Dev

1.  **Docker Compose:** Essential for defining and running multi-service applications (e.g., a frontend, a backend API, and a database).
2.  **Bind Mounts:** This is critical for local development. By mounting your local source code directory into the container, any changes you make on your host machine are immediately reflected inside the container. This enables hot-reloading or live-reloading for frontend applications.
    *   **Excluding `node_modules`:** When bind mounting, it's common to exclude the `node_modules` directory from the host mount to prevent issues with different OS architectures or to ensure container-specific dependencies are used. This is often done with an anonymous volume.
3.  **Port Mapping:** Map container ports to host ports so you can access your application from your browser (e.g., `localhost:3000`).
4.  **Environment Variables:** Use environment variables to configure development-specific settings (e.g., `NODE_ENV=development`, API endpoints).

## Code Example

### `docker-compose.yml` for a React Frontend and Node.js Backend

```yaml
# docker-compose.dev.yml (or just docker-compose.yml if only for dev)
version: '3.8'
services:
  frontend:
    build:
      context: .
      dockerfile: Dockerfile.frontend.dev # A Dockerfile optimized for dev
    ports:
      - "3000:3000" # Map host port 3000 to container port 3000
    volumes:
      - .:/app # Mount current host directory to /app in container
      - /app/node_modules # Exclude node_modules from host mount
    environment:
      NODE_ENV: development
      CHOKIDAR_USEPOLLING: "true" # For some hot-reloading setups on certain OS
    depends_on:
      - backend

  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile.backend.dev # A Dockerfile optimized for dev
    ports:
      - "5000:5000"
    volumes:
      - ./backend:/app # Mount backend directory for development
      - /app/node_modules # Exclude node_modules
    environment:
      NODE_ENV: development
      DATABASE_URL: postgres://user:password@db:5432/mydb
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

### `Dockerfile.frontend.dev` (for a React app)

```dockerfile
# Dockerfile.frontend.dev
FROM node:18-alpine
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install # Install dev dependencies
COPY . .
EXPOSE 3000
CMD ["yarn", "start"]
```

**To start your local development environment:**

1.  Place `docker-compose.dev.yml` and `Dockerfile.frontend.dev` (and `Dockerfile.backend.dev` if applicable) in your project.
2.  Run `docker-compose -f docker-compose.dev.yml up`

Now, your frontend will be accessible at `http://localhost:3000` and your backend at `http://localhost:5000`.

## Resources

*   **Article:** [Docker Docs - Develop with Docker Compose](https://docs.docker.com/compose/gettingstarted/)
*   **Article:** [Local Development with Docker Compose for Frontend Projects](https://www.freecodecamp.org/news/local-development-with-docker-compose-for-frontend-projects/)
*   **Video:** [Docker Compose for Local Development - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
