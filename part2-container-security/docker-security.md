# Docker Security Best Practices

To secure containerized environments, follow these best practices:

## 1. Use Minimal Base Images
- Use images like `alpine`, `distroless`, or scratch to reduce surface area.
- Smaller images = fewer packages = fewer vulnerabilities.

## 2. Run as a Non-Root User
- Avoid `root` in containers; use `USER` directive in Dockerfile.
- Helps prevent privilege escalation if the container is compromised.

## 3. Use Multi-Stage Builds
- Separate build tools and dependencies from final runtime.
- Reduces image size and exposure.

## 4. Scan Images for Vulnerabilities
- Use tools like:
  - `Trivy`
  - `Grype`
  - Amazon Inspector (ECR scan)

## 5. Enforce Resource Limits
- Set memory and CPU limits in Kubernetes or Docker Compose.
- Prevents resource exhaustion and DoS attacks.

---

### Example Secure Dockerfile

```Dockerfile
# Stage 1: Build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Run
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm install --omit=dev

# Add non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

CMD ["node", "dist/index.js"]
```
