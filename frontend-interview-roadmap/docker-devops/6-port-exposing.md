
# 6. Port Exposing in Docker

## Quick Revision

**Port exposing** in Docker is the process of making a port inside a Docker container accessible from the host machine or from other containers. This is essential for any network-enabled application running within a container, such as a web server, API, or database.

*   **`EXPOSE` (Dockerfile instruction):** Documents which ports the application inside the container listens on. It does not actually publish the port.
*   **`-p` or `--publish` (Docker CLI option):** Publishes a container's port(s) to the host. This is what actually makes the port accessible from outside the container.

## Detailed Explanation

When you run an application inside a Docker container, it runs in an isolated network environment. By default, ports opened by the application inside the container are not accessible from the host machine or the outside world.

### `EXPOSE` Instruction in Dockerfile

*   **Purpose:** The `EXPOSE` instruction in a `Dockerfile` serves as documentation. It informs anyone building or running the image that the application inside the container intends to listen on the specified port(s).
*   **Functionality:** It does **not** publish the port to the host machine. It only makes the port available for inter-container communication within a Docker network.
*   **Example:** `EXPOSE 3000`

### `-p` or `--publish` Option in `docker run`

*   **Purpose:** The `-p` (or `--publish`) option in the `docker run` command is used to actually publish a container's port(s) to the host machine. This creates a mapping between a port on the host and a port inside the container.
*   **Syntax:** `docker run -p <host_port>:<container_port> <image_name>`
*   **Example:** `docker run -p 80:3000 my-frontend-app`
    *   This maps port `80` on the host to port `3000` inside the container. So, if your application inside the container is listening on port `3000`, you can access it from your host machine at `http://localhost:80`.

### Port Mapping in Docker Compose

In `docker-compose.yml`, you use the `ports` key to define port mappings.

*   **Syntax:**

    ```yaml
    ports:
      - "<host_port>:<container_port>"
      - "<container_port>" # Docker will assign a random host port
    ```

*   **Example:**

    ```yaml
    services:
      frontend:
        image: my-frontend-app
        ports:
          - "3000:80" # Map host port 3000 to container port 80
    ```

## Code Examples

### Dockerfile with `EXPOSE`

```dockerfile
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
EXPOSE 3000 # Documents that the app listens on port 3000
CMD ["npm", "start"]
```

### Running with Port Publishing

```bash
# Build the image
docker build -t my-node-app .

# Run the container, mapping host port 8080 to container port 3000
docker run -p 8080:3000 my-node-app
```

Now, if your Node.js app inside the container is listening on port `3000`, you can access it from your host machine at `http://localhost:8080`.

### Docker Compose Port Mapping

```yaml
# docker-compose.yml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "80:3000" # Host port 80 -> Container port 3000
      - "443:443" # Host port 443 -> Container port 443 (for HTTPS)
    environment:
      PORT: 3000 # Ensure your app listens on this port inside the container
```

## Resources

*   **Article:** [Docker Docs - `EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose)
*   **Article:** [Docker Docs - `docker run --publish`](https://docs.docker.com/engine/reference/commandline/run/#publish)
*   **Article:** [Docker Docs - Compose file ports](https://docs.docker.com/compose/compose-file/compose-file-v3/#ports)
*   **Video:** [Docker Ports Explained - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
