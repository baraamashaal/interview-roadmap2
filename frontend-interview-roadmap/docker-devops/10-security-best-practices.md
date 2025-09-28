
# 10. Security Best Practices for Docker

## Quick Revision

**Docker security best practices** focus on minimizing the attack surface, ensuring the integrity of images and containers, and protecting sensitive data. This is crucial for preventing vulnerabilities that could compromise your applications and infrastructure.

Key practices include:

*   **Use minimal base images:** Reduce the attack surface.
*   **Avoid running as root:** Use a non-root user.
*   **Scan images for vulnerabilities:** Identify and fix known issues.
*   **Use multi-stage builds:** Exclude build tools and sensitive data from the final image.
*   **Manage secrets securely:** Don't hardcode sensitive information.
*   **Implement resource limits:** Prevent resource exhaustion attacks.

## Detailed Explanation

Docker containers provide a layer of isolation, but they are not inherently secure. Following best practices is essential to mitigate risks.

### 1. Use Minimal Base Images

*   **Why:** Smaller images have fewer packages, which means fewer potential vulnerabilities and a smaller attack surface.
*   **How:** Use `alpine` variants (e.g., `node:18-alpine`, `nginx:stable-alpine`) or `scratch` for extremely minimal images.

### 2. Avoid Running as Root

*   **Why:** Running processes as `root` inside a container can pose a security risk. If an attacker gains control of a root process in a container, they might be able to escalate privileges on the host system.
*   **How:** Create a non-root user in your `Dockerfile` and switch to it using the `USER` instruction.

    ```dockerfile
    FROM node:18-alpine
    WORKDIR /app
    COPY package.json ./
    RUN npm install
    COPY . .
    RUN npm run build

    # Create a non-root user
    RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
    USER appuser

    EXPOSE 3000
    CMD ["npm", "start"]
    ```

### 3. Scan Images for Vulnerabilities

*   **Why:** Docker images can contain known vulnerabilities from their base layers or installed packages.
*   **How:** Use tools like `Trivy`, `Clair`, or Docker Scout to scan your images for vulnerabilities. Integrate these scans into your CI/CD pipeline.

### 4. Use Multi-Stage Builds

*   **Why:** Multi-stage builds ensure that your final production image only contains the necessary runtime artifacts, leaving behind build tools, development dependencies, and any sensitive data used during the build process.
*   **How:** Separate your `Dockerfile` into `builder` and `runner` stages. (See question 4 for more details).

### 5. Manage Secrets Securely

*   **Why:** Hardcoding sensitive information (API keys, database credentials) in your `Dockerfile` or application code is a major security risk.
*   **How:**
    *   **Environment Variables:** Pass secrets as environment variables at runtime (e.g., `docker run -e MY_SECRET=value`).
    *   **Docker Secrets:** For more robust secret management in production, use Docker Secrets (for Docker Swarm) or Kubernetes Secrets.
    *   **Vault/AWS Secrets Manager:** Integrate with dedicated secret management services.

### 6. Implement Resource Limits

*   **Why:** Unrestricted containers can consume excessive CPU or memory, leading to denial-of-service (DoS) attacks or impacting other services on the host.
*   **How:** Use Docker's resource limits (`--memory`, `--cpus`) when running containers.

    ```bash
docker run --memory="512m" --cpus="0.5" my-app
    ```

### 7. Sign and Verify Images

*   **Why:** Ensure that the images you are using are authentic and haven't been tampered with.
*   **How:** Use Docker Content Trust to sign and verify images.

## Resources

*   **Article:** [Docker Docs - Security](https://docs.docker.com/engine/security/)
*   **Article:** [Docker Docs - Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
*   **Tool:** [Trivy (Vulnerability Scanner)](https://aquasecurity.github.io/trivy/v0.18.3/)
*   **Video:** [Docker Security Best Practices - Traversy Media](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
