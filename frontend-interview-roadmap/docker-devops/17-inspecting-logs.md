
# 17. Inspecting Logs in Docker

## Quick Revision

**Inspecting logs** in Docker is crucial for debugging, monitoring, and understanding the behavior of your applications running inside containers. Docker provides a simple command-line interface to access the standard output (`stdout`) and standard error (`stderr`) streams of your containers.

## Detailed Explanation

When an application runs inside a Docker container, its output (logs) are typically directed to `stdout` and `stderr`. Docker captures these streams, allowing you to view them using the `docker logs` command.

### `docker logs` Command

The `docker logs` command is the primary way to retrieve logs from a container. It has several useful options:

*   **`docker logs [OPTIONS] CONTAINER`:** Retrieves logs from a specified container.
*   **`-f` or `--follow`:** Follows log output in real-time (like `tail -f`).
*   **`--since TIME`:** Show logs since a specific timestamp or relative duration (e.g., `10m` for 10 minutes, `1h` for 1 hour).
*   **`--until TIME`:** Show logs before a specific timestamp or relative duration.
*   **`-n` or `--tail NUMBER`:** Show only the last `NUMBER` of log lines.
*   **`-t` or `--timestamps`:** Show timestamps in the logs.
*   **`--details`:** Show extra details provided to logs.

### Log Drivers

Docker uses **log drivers** to manage where and how logs are stored. The default log driver is `json-file`, which stores logs in JSON format on the host machine. Other popular log drivers include:

*   **`json-file`:** Default, stores logs as JSON files.
*   **`syslog`:** Sends logs to a syslog server.
*   **`journald`:** Sends logs to the systemd journal.
*   **`gelf`:** Sends logs to a Graylog Extended Log Format (GELF) endpoint.
*   **`awslogs`:** Sends logs to Amazon CloudWatch Logs.

You can configure the log driver for a container or service in `docker run` or `docker-compose.yml`.

## Code Examples

### Viewing Logs of a Running Container

First, let's assume you have a simple Node.js application running in a container:

```javascript
// app.js
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  console.log('Request received for /');
  res.send('Hello from Docker!');
});

app.listen(port, () => {
  console.log(`App listening at http://localhost:${port}`);
});
```

```dockerfile
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json ./
RUN npm install express
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

```bash
# Build and run the container
docker build -t my-node-app .
docker run -p 3000:3000 -d --name my-node-container my-node-app
```

Now, to inspect its logs:

```bash
# View all logs from the container
docker logs my-node-container

# Follow logs in real-time
docker logs -f my-node-container

# Show the last 10 lines of logs with timestamps
docker logs --tail 10 -t my-node-container

# Show logs since 5 minutes ago
docker logs --since 5m my-node-container
```

### Configuring Log Driver in Docker Compose

```yaml
version: '3.8'
services:
  web:
    image: my-node-app
    ports:
      - "3000:3000"
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
  backend:
    image: my-backend-app
    logging:
      driver: "syslog"
      options:
        syslog-address: "udp://192.168.1.100:514"
```

## Resources

*   **Article:** [Docker Docs - `docker logs`](https://docs.docker.com/engine/reference/commandline/logs/)
*   **Article:** [Docker Docs - Configure logging drivers](https://docs.docker.com/config/containers/logging/configure/)
*   **Video:** [Docker Logs Explained - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
