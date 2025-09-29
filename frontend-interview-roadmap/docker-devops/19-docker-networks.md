
# 19. Docker Networks

## Quick Revision

**Docker networks** enable communication between Docker containers and between containers and the host machine. Docker provides several built-in network drivers, and you can also create custom networks to isolate and organize your services.

Common network drivers:

*   **`bridge`:** The default network driver. Containers on the same bridge network can communicate with each other.
*   **`host`:** Removes network isolation between the container and the Docker host, allowing the container to use the host's network stack directly.
*   **`none`:** Disables all networking for the container.
*   **`overlay`:** Used for multi-host container communication in Docker Swarm.

## Detailed Explanation

Networking is a critical aspect of running multi-container applications. Docker's networking capabilities allow you to define how your services discover and communicate with each other securely.

### 1. Bridge Networks (Default)

*   **How it works:** When you install Docker, a default bridge network (`bridge`) is created. Containers connected to this bridge network can communicate with each other using their IP addresses. Docker also provides DNS resolution, allowing containers to communicate by their container names (if linked or part of a Compose project).
*   **Use Cases:** Single-host applications where containers need to communicate with each other.

### 2. User-Defined Bridge Networks

*   **How it works:** You can create your own custom bridge networks. This provides better isolation and automatic DNS resolution between containers connected to the same user-defined network.
*   **Benefits:**
    *   **Automatic DNS resolution:** Containers can resolve each other by name.
    *   **Better isolation:** Containers on different user-defined networks are isolated by default.
    *   **Configurable:** You can configure network settings like subnets and gateways.
*   **Creation:** `docker network create my-custom-network`

### 3. Host Network

*   **How it works:** A container using the host network shares the network namespace of the host machine. This means the container's ports are directly exposed on the host's IP address.
*   **Use Cases:** When you need the container to have direct access to the host's network interfaces, or for performance-critical applications where network overhead needs to be minimized.
*   **Caution:** Reduces network isolation.

### 4. None Network

*   **How it works:** A container connected to the `none` network has no network interfaces (only a loopback interface).
*   **Use Cases:** For containers that don't require network access, or for security-sensitive tasks where network isolation is paramount.

### 5. Overlay Networks

*   **How it works:** Overlay networks enable communication between containers running on different Docker hosts. They are primarily used in Docker Swarm mode for orchestrating multi-host applications.

## Code Examples

### Creating and Using a Custom Bridge Network

```bash
# Create a custom bridge network
docker network create my-app-network

# Run a database container on the custom network
docker run -d --name my-db --network my-app-network postgres:13

# Run a backend container on the custom network, linking to the database by name
docker run -d --name my-backend --network my-app-network -e DB_HOST=my-db my-backend-image

# Run a frontend container on the custom network
docker run -d --name my-frontend --network my-app-network -p 80:80 my-frontend-image
```

### Docker Compose with Custom Networks

```yaml
version: '3.8'
services:
  frontend:
    build: ./frontend
    ports:
      - "3000:80"
    networks:
      - app-network

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      DB_HOST: db
    networks:
      - app-network

  db:
    image: postgres:13
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```

**Explanation:**

*   All services (`frontend`, `backend`, `db`) are connected to the `app-network`.
*   They can communicate with each other using their service names (e.g., `backend` can reach the database at `db:5432`).

## Resources

*   **Article:** [Docker Docs - Networking overview](https://docs.docker.com/network/)
*   **Article:** [Docker Docs - Bridge networks](https://docs.docker.com/network/bridge/)
*   **Video:** [Docker Networking Explained - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
