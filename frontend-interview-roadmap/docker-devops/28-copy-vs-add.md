
# 28. `COPY` vs. `ADD` in Dockerfiles

## Quick Revision

Both **`COPY`** and **`ADD`** are `Dockerfile` instructions used to copy files and directories from the host machine into the Docker image. While they seem similar, they have key differences in their capabilities and recommended use cases.

*   **`COPY`:** Copies local files or directories from the build context to the image. It's generally preferred for simple file transfers.

*   **`ADD`:** Has additional features:
    *   Can extract compressed archives (tar, gzip, bzip2) from the source to the destination.
    *   Can fetch files from remote URLs.

## Detailed Explanation

### `COPY` Instruction

*   **Syntax:** `COPY <src>... <dest>` or `COPY ["<src>",... "<dest>"]`
*   **Source (`<src>`):** Must be a path to a file or directory on the host machine relative to the build context.
*   **Destination (`<dest>`):** An absolute path or a path relative to the `WORKDIR` inside the image.
*   **Behavior:** Simply copies files and directories as-is.
*   **Best Practice:** `COPY` is generally preferred because it's more transparent. It only copies local files, making it clear what's being added to the image.

### `ADD` Instruction

*   **Syntax:** `ADD <src>... <dest>` or `ADD ["<src>",... "<dest>"]`
*   **Source (`<src>`):** Can be a path to a file/directory relative to the build context, or a URL.
*   **Destination (`<dest>`):** An absolute path or a path relative to the `WORKDIR` inside the image.
*   **Additional Features:**
    *   **Tar Extraction:** If `<src>` is a compressed archive (tar, gzip, bzip2) and `<dest>` is a directory, `ADD` will automatically extract the archive.
    *   **Remote URLs:** If `<src>` is a URL, `ADD` will download the file from that URL and place it at `<dest>`.
*   **Best Practice:** Use `ADD` only when you need its special features (auto-extraction or remote URL fetching). Otherwise, `COPY` is recommended for clarity and predictability.

### Security and Caching Considerations

*   **`ADD` with URLs:** Downloading files from remote URLs with `ADD` can introduce security risks if the source is untrusted. It also creates an extra layer that might not be cached efficiently.
*   **Cache Invalidation:** Both `COPY` and `ADD` invalidate the build cache from their layer onwards if the source content changes.

## Code Examples

### `COPY` Example

```dockerfile
FROM node:18-alpine
WORKDIR /app

# Copy package.json and yarn.lock to install dependencies
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# Copy the rest of the application code
COPY . .

EXPOSE 3000
CMD ["yarn", "start"]
```

### `ADD` Example (Extracting a Tarball)

```dockerfile
FROM ubuntu:20.04
WORKDIR /app

# Assume my-app.tar.gz is in the build context
ADD my-app.tar.gz /app/

# The contents of my-app.tar.gz will be extracted into /app

CMD ["./my-app/start.sh"]
```

### `ADD` Example (Downloading from URL - Less Recommended)

```dockerfile
FROM ubuntu:20.04
WORKDIR /app

# Downloads a file from a URL (less recommended for security/caching)
ADD https://example.com/some-config.conf /etc/some-config.conf

CMD ["bash"]
```

**Note:** For downloading files from URLs, it's often better to use `RUN curl -LO <URL> && mv <file> <dest>` as it gives you more control over caching and error handling.

## Resources

*   **Article:** [Docker Docs - `COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy)
*   **Article:** [Docker Docs - `ADD` instruction](https://docs.docker.com/engine/reference/builder/#add)
*   **Article:** [Docker `COPY` vs `ADD`: What's the Difference?](https://www.freecodecamp.org/news/docker-copy-vs-add-whats-the-difference/)
*   **Video:** [Docker COPY vs ADD - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
