
# 14. Environment Variables in Docker

## Quick Revision

**Environment variables** in Docker are a fundamental way to configure containers at runtime. They allow you to pass dynamic configuration to your applications without modifying the Docker image itself. This is crucial for managing different settings across various environments (development, staging, production) and for securely injecting sensitive information.

## Detailed Explanation

Environment variables provide a flexible mechanism to externalize configuration from your Docker images. This adheres to the 12-factor app methodology, promoting a clean separation of configuration from code.

### How Environment Variables Work in Docker

1.  **`ENV` instruction in Dockerfile:** Sets environment variables during the image build process. These variables are then available to all subsequent instructions in the `Dockerfile` and to the running container.

    ```dockerfile
    ENV NODE_ENV production
    ENV PORT 3000
    ```

2.  **`-e` or `--env` option in `docker run`:** Passes environment variables to a container at runtime. These variables override any `ENV` instructions defined in the `Dockerfile`.

    ```bash
docker run -e MY_API_KEY=12345 -e DB_HOST=production-db my-app
    ```

3.  **`--env-file` option in `docker run`:** Loads environment variables from a file.

    ```bash
docker run --env-file ./config.env my-app
    ```

4.  **`environment` key in `docker-compose.yml`:** Defines environment variables for services in a Compose file.

    ```yaml
    services:
      backend:
        environment:
          NODE_ENV: production
          DB_HOST: db
    ```

### Security Considerations

*   **Avoid hardcoding secrets:** Never hardcode sensitive information (API keys, passwords) directly into your `Dockerfile` or application code.
*   **Don't commit `.env` files:** Use `.dockerignore` to prevent `.env` files from being copied into your image or build context.
*   **Use Docker Secrets or Kubernetes Secrets:** For production environments, use dedicated secret management solutions to inject sensitive data into containers securely.
*   **Minimize `ENV` in Dockerfile:** While `ENV` is useful for non-sensitive configuration, avoid putting secrets there as they become part of the image layer history.

## Code Examples

### Dockerfile with `ENV`

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .

ENV NODE_ENV production # Set default environment
ENV PORT 3000 # Set default port

EXPOSE $PORT
CMD ["npm", "start"]
```

### Overriding `ENV` with `docker run`

```bash
# Build the image
docker build -t my-node-app .

# Run the container, overriding NODE_ENV and PORT
docker run -p 8080:4000 -e NODE_ENV=development -e PORT=4000 my-node-app
```

### Using `.env` file with `docker run`

Create a `config.env` file:

```
# config.env
MY_API_KEY=supersecretkey
DB_USER=admin
```

Then run:

```bash
docker run --env-file ./config.env my-app
```

### `docker-compose.yml` with Environment Variables

```yaml
version: '3.8'
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      NODE_ENV: development
      DATABASE_URL: postgres://user:password@db:5432/mydb
      # You can also load from a .env file for the service
      # env_file:
      #   - ./.env.backend
```

## Resources

*   **Article:** [Docker Docs - `ENV` instruction](https://docs.docker.com/engine/reference/builder/#env)
*   **Article:** [Docker Docs - Environment variables in Compose](https://docs.docker.com/compose/compose-file/compose-file-v3/#environment)
*   **Article:** [Docker Docs - Manage sensitive data with Docker secrets](https://docs.docker.com/engine/swarm/secrets/)
*   **Video:** [Docker Environment Variables - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
