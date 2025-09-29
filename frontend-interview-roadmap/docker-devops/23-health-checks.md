# 23. Health Checks in Docker

## Quick Revision

**Health checks** in Docker allow you to specify a command that Docker should run inside a container to determine if the application running within it is still healthy and responsive. This is crucial for ensuring the reliability and availability of your services, especially in orchestrated environments like Docker Swarm or Kubernetes.

## Detailed Explanation

By default, Docker only checks if a container's main process is running. If the process is still active, Docker considers the container to be "up." However, the application inside the container might be frozen, unresponsive, or stuck in a loop, even if its process is technically running.

Health checks provide a more robust way to determine the actual health of your application.

### How Docker Health Checks Work

1.  **`HEALTHCHECK` instruction in Dockerfile:** You define a `HEALTHCHECK` instruction in your `Dockerfile`.
2.  **Command Execution:** Docker periodically runs the specified command inside the container.
3.  **Exit Code Interpretation:**
    *   **`0`:** Success - the container is healthy.
    *   **`1`:** Failure - the container is unhealthy.
    *   **`2`:** Reserved - do not use.
4.  **Status Update:** Based on the exit code, Docker updates the container's health status (e.g., `healthy`, `unhealthy`, `starting`).

### `HEALTHCHECK` Options

*   **`--interval=DURATION`:** How often to run the check (default: 30s).
*   **`--timeout=DURATION`:** How long the check can take before it's considered failed (default: 30s).
*   **`--start-period=DURATION`:** Grace period for the container to start up before health checks begin (default: 0s).
*   **`--retries=N`:** How many consecutive failures are needed to consider the container unhealthy (default: 3).

### Benefits

*   **Improved Reliability:** Docker (and orchestrators) can automatically restart unhealthy containers.
*   **Faster Recovery:** Reduces downtime by quickly identifying and replacing failed services.
*   **Better Monitoring:** Provides a clear health status for your containers.

## Code Example

### Dockerfile with `HEALTHCHECK` for a Node.js App

Let's assume your Node.js application exposes a health endpoint at `/health` that returns a 200 status code when healthy.

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
EXPOSE 3000

# Healthcheck instruction
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1

CMD ["npm", "start"]
```

**Explanation:**

*   Docker will run `curl -f http://localhost:3000/health` every 30 seconds.
*   If `curl` returns a non-zero exit code (e.g., if the endpoint is not reachable or returns an error status), the health check fails.
*   The container gets a 5-second grace period (`start-period`) before checks begin.
*   After 3 consecutive failures (`retries=3`), the container will be marked as `unhealthy`.

### Viewing Health Status

```bash
# Run the container
docker run -d --name my-healthy-app my-image

# Check the health status
docker ps
# Output will show something like: Up 10 seconds (healthy)

# Inspect container details, including healthcheck results
docker inspect my-healthy-app
```

### Docker Compose with Health Checks

```yaml
version: '3.8'
services:
  frontend:
    image: my-frontend-app
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost/health"]
      interval: 1m30s
      timeout: 10s
      retries: 3
      start_period: 30s

  backend:
    image: my-backend-app
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user -d mydb"]
      interval: 5s
      timeout: 5s
      retries: 5
```

## Resources

*   **Article:** [Docker Docs - `HEALTHCHECK` instruction](https://docs.docker.com/engine/reference/builder/#healthcheck)
*   **Article:** [Docker Docs - Healthcheck in Compose](https://docs.docker.com/compose/compose-file/compose-file-v3/#healthcheck)
*   **Video:** [Docker Health Checks Explained - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
