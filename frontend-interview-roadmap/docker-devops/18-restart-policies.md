
# 18. Docker Restart Policies

## Quick Revision

**Docker restart policies** control how containers behave when they exit, or when the Docker daemon restarts. They ensure that your services remain available and resilient to failures. You can configure a restart policy when you run a container using `docker run` or define it in your `docker-compose.yml`.

Common policies include:

*   **`no`:** Do not automatically restart the container (default).
*   **`on-failure`:** Restart only if the container exits with a non-zero exit code (indicating an error).
*   **`always`:** Always restart the container, even if it exits cleanly. It will also restart when Docker daemon starts.
*   **`unless-stopped`:** Always restart the container unless it is explicitly stopped by the user.

## Detailed Explanation

In a production environment, you want your applications to be highly available. If a container crashes or the Docker daemon restarts, you need a mechanism to automatically bring your services back online. Docker restart policies provide this functionality.

### How Restart Policies Work

When you specify a restart policy for a container, Docker monitors its state. If the container stops for any reason (e.g., application crash, host reboot), Docker will attempt to restart it according to the defined policy.

### Available Restart Policies

1.  **`no` (Default):** The container will not be automatically restarted by Docker. You have to manually start it.

2.  **`on-failure[:max-retries]`:** The container will only be restarted if it exits with a non-zero exit code (indicating an error). You can optionally specify `max-retries` to limit the number of restart attempts.

    *   Example: `on-failure:5` (Docker will try to restart the container up to 5 times).

3.  **`always`:** The container will always be restarted if it stops, regardless of the exit code. It will also restart when the Docker daemon starts (e.g., after a host reboot).

4.  **`unless-stopped`:** The container will always be restarted unless it is explicitly stopped by the user (e.g., `docker stop <container>`). If the Docker daemon restarts, the container will also restart.

### Choosing the Right Policy

*   **`no`:** For development or one-off tasks where you don't need automatic restarts.
*   **`on-failure`:** For applications that might occasionally crash but you want them to recover automatically.
*   **`always` or `unless-stopped`:** For production services that need to be continuously running and resilient to failures. `unless-stopped` is often preferred as it gives you more control if you manually stop a container.

## Code Examples

### Using `docker run`

```bash
# Run a container with the 'always' restart policy
docker run -d --restart always --name my-web-app my-image

# Run a container with 'on-failure' policy, max 3 retries
docker run -d --restart on-failure:3 --name my-backend-service my-image
```

### Using `docker-compose.yml`

```yaml
version: '3.8'
services:
  frontend:
    image: my-frontend-app
    ports:
      - "3000:80"
    restart: unless-stopped # Always restart unless explicitly stopped

  backend:
    image: my-backend-app
    ports:
      - "5000:5000"
    restart: on-failure:5 # Restart on error, up to 5 times

  database:
    image: postgres:13
    restart: always # Always restart the database
```

## Resources

*   **Article:** [Docker Docs - Start containers automatically](https://docs.docker.com/config/containers/start-containers-automatically/)
*   **Video:** [Docker Restart Policies Explained - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
