
# 29. Docker Image Security Scanning

## Quick Revision

**Docker image security scanning** is the process of analyzing Docker images for known vulnerabilities, misconfigurations, and security best practice violations. This is a critical step in securing your containerized applications, as images often contain numerous layers and dependencies that can introduce security risks.

## Detailed Explanation

Docker images are built from layers, and each layer can introduce vulnerabilities. These vulnerabilities can come from:

*   **Base images:** The operating system or runtime chosen (e.g., `ubuntu`, `node:alpine`).
*   **Installed packages:** Libraries and tools installed via `apt-get`, `apk`, `npm`, `yarn`, etc.
*   **Application code:** Your own code can have security flaws.
*   **Misconfigurations:** Incorrectly configured services or permissions.

Security scanning helps identify these issues early in the development lifecycle, ideally as part of your CI/CD pipeline.

### Types of Scans

1.  **Vulnerability Scanning:** Detects known vulnerabilities (CVEs - Common Vulnerabilities and Exposures) in the operating system packages and application dependencies within your image.
2.  **Configuration Scanning:** Checks for misconfigurations or deviations from security best practices (e.g., running as root, exposed sensitive ports).
3.  **Secret Detection:** Scans for hardcoded secrets (API keys, passwords) that might have accidentally been included in the image.

### Popular Scanning Tools

*   **Trivy:** An open-source, comprehensive, and easy-to-use vulnerability scanner for container images, filesystems, and Git repositories. It detects OS packages and application dependencies.
*   **Clair:** An open-source project for the static analysis of vulnerabilities in application containers.
*   **Snyk:** A commercial tool that integrates with various platforms and provides vulnerability scanning for code, dependencies, and Docker images.
*   **Docker Scout:** Docker's own tool for image analysis and vulnerability management.

### Integration into CI/CD

Integrating security scanning into your CI/CD pipeline is a best practice. This ensures that every new image built is automatically scanned, and builds can be failed if critical vulnerabilities are found.

## Code Example (Using Trivy in a CI/CD Pipeline)

Let's assume you have a `Dockerfile` and a GitHub Actions workflow.

```yaml
# .github/workflows/docker-scan.yml
name: Docker Image Security Scan

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Build Docker image
        run: docker build -t my-frontend-app:latest .

      - name: Run Trivy vulnerability scan
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: 'my-frontend-app:latest'
          format: 'table'
          exit-code: '1' # Fail the build if vulnerabilities are found
          severity: 'CRITICAL,HIGH' # Only report Critical and High severity vulnerabilities

      # Example: Push image only if scan passes
      # - name: Log in to Docker Hub
      #   uses: docker/login-action@v2
      #   with:
      #     username: ${{ secrets.DOCKER_USERNAME }}
      #     password: ${{ secrets.DOCKER_PASSWORD }}
      # - name: Push Docker image
      #   run: docker push my-frontend-app:latest
```

**Explanation:**

*   The workflow builds the Docker image.
*   It then runs `Trivy` to scan the `my-frontend-app:latest` image.
*   The `exit-code: '1'` and `severity: 'CRITICAL,HIGH'` ensure that the CI build will fail if any critical or high-severity vulnerabilities are detected.

## Resources

*   **Tool:** [Trivy](https://aquasecurity.github.io/trivy/)
*   **Tool:** [Snyk Container](https://snyk.io/product/container-security/)
*   **Article:** [Docker Docs - Security scanning](https://docs.docker.com/engine/scan/)
*   **Video:** [Container Security Scanning with Trivy - TechWorld with Nana](https://www.youtube.com/watch?v=static-relative-absolute-fixed-sticky)
