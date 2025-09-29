
# 27. `ENTRYPOINT` vs. `CMD` in Docker

## Quick Revision

Both `ENTRYPOINT` and `CMD` are `Dockerfile` instructions used to define the command that will be executed when a Docker container starts. However, they have distinct behaviors and use cases.

*   **`CMD`:** Provides default arguments for an executing container. These arguments can be easily overridden when running the container.

*   **`ENTRYPOINT`:** Configures a container that will run as an executable. It sets the primary command that will always be executed when the container starts.

## Detailed Explanation

Understanding the difference between `ENTRYPOINT` and `CMD` is crucial for building flexible and robust Docker images.

### `CMD` (Command)

*   **Purpose:** To provide default arguments for an executing container. If you specify a command when running the container, it will override the `CMD` instruction.
*   **Format:**
    *   **Exec form (recommended):** `CMD ["executable","param1","param2"]`
    *   **Shell form:** `CMD command param1 param2` (runs in a shell, e.g., `/bin/sh -c command`)
*   **Behavior:**
    *   If `docker run` specifies a command, `CMD` is ignored.
    *   If `docker run` does not specify a command, `CMD` is executed.
    *   If `ENTRYPOINT` is defined, `CMD` provides default arguments to the `ENTRYPOINT`.
*   **Only one `CMD`:** A `Dockerfile` can only have one `CMD` instruction. If multiple are listed, only the last one takes effect.

### `ENTRYPOINT` (Entrypoint)

*   **Purpose:** To configure a container that will run as an executable. It defines the primary command that will always be executed when the container starts.
*   **Format:**
    *   **Exec form (recommended):** `ENTRYPOINT ["executable","param1","param2"]`
    *   **Shell form:** `ENTRYPOINT command param1 param2` (runs in a shell)
*   **Behavior:**
    *   The `ENTRYPOINT` command is always executed when the container starts.
    *   If `CMD` is also defined, its values are passed as arguments to the `ENTRYPOINT` command.
    *   Arguments passed to `docker run` are appended to the `ENTRYPOINT` command, overriding the `CMD`.
*   **Only one `ENTRYPOINT`:** A `Dockerfile` can only have one `ENTRYPOINT` instruction.

### When to Use Which

*   **Use `CMD`:**
    *   When you need to provide default arguments to an executable.
    *   When you want the user to easily override the default command.
*   **Use `ENTRYPOINT`:**
    *   When you want to make your image behave like an executable (e.g., a utility image).
    *   When you want to ensure a specific command is always run, and `CMD` provides its default parameters.

## Code Examples

### `CMD` Example

```dockerfile
# Dockerfile
FROM ubuntu:latest
CMD ["echo", "Hello, Docker!"]
```

```bash
# Run with default CMD
docker run my-image # Output: Hello, Docker!

# Override CMD with a new command
docker run my-image ls -l / # Output: directory listing
```

### `ENTRYPOINT` Example

```dockerfile
# Dockerfile
FROM ubuntu:latest
ENTRYPOINT ["echo"]
CMD ["Hello, Docker!"]
```

```bash
# Run with default CMD as argument to ENTRYPOINT
docker run my-image # Output: Hello, Docker!

# Pass new arguments to ENTRYPOINT, overriding CMD
docker run my-image "Custom message!" # Output: Custom message!

# Override ENTRYPOINT (less common)
docker run --entrypoint bash my-image
```

### Common Pattern: `ENTRYPOINT` + `CMD`

This is a very common and flexible pattern, especially for applications.

```dockerfile
# Dockerfile for a Node.js app
FROM node:18-alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
EXPOSE 3000

ENTRYPOINT ["node"]
CMD ["server.js"]
```

```bash
# Runs: node server.js
docker run my-node-app

# Runs: node debug.js (overrides CMD)
docker run my-node-app debug.js

# Runs: bash (overrides ENTRYPOINT and CMD)
docker run --entrypoint bash my-node-app
```

## Resources

*   **Article:** [Docker Docs - `CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd)
*   **Article:** [Docker Docs - `ENTRYPOINT` instruction](https://docs.docker.com/engine/reference/builder/#entrypoint)
*   **Article:** [Understanding `CMD` and `ENTRYPOINT` in Docker](https://www.freecodecamp.org/news/understanding-cmd-and-entrypoint-in-docker/)
*   **Video:** [Docker CMD vs ENTRYPOINT - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
