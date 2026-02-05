#### Dockerfile 
```dockerfile
# Use official Python base image
FROM python:3.11-slim

# Set metadata
LABEL maintainer="prasanth@example.com"

# Set working directory
WORKDIR /app

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Copy dependency file first (layer caching)
COPY requirements.txt .

# Install system packages (optional but common)
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc && \
    pip install --no-cache-dir -r requirements.txt && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy application source code
COPY . .

# Expose application port
EXPOSE 8000

# Health check (optional)
HEALTHCHECK CMD python --version || exit 1

# Default command to run the app
CMD ["python", "app.py"]
```

---

#### Short Explanation of Dockerfile Commands

* **FROM** – Defines the base image for Python runtime
* **LABEL** – Adds metadata about the image
* **WORKDIR** – Sets the working directory inside the container
* **ENV** – Sets environment variables for Python behavior
* **COPY** – Copies files from host to container
* **RUN** – Executes commands during image build (install packages, dependencies)
* **EXPOSE** – Documents the port used by the application
* **HEALTHCHECK** – Checks container health status
* **CMD** – Default command executed when the container starts

#### Multi-Stage Dockerfile 

```dockerfile
# =========================
# Stage 1: Builder
# =========================
FROM python:3.11-slim AS builder

# Set working directory
WORKDIR /app

# Prevent Python from writing pyc files & enable unbuffered logs
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Install build dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc build-essential && \
    rm -rf /var/lib/apt/lists/*

# Copy dependency file
COPY requirements.txt .

# Install Python dependencies into a virtual directory
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt


# =========================
# Stage 2: Runtime
# =========================
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Copy installed dependencies from builder stage
COPY --from=builder /install /usr/local

# Copy application source code
COPY . .

# Expose application port
EXPOSE 8000

# Health check
HEALTHCHECK CMD python --version || exit 1

# Run the application
CMD ["python", "app.py"]
```

---

#### Short Explanation (Multi-Stage Concepts)

* **Stage 1 (Builder)** – Installs build tools and Python dependencies
* **AS builder** – Names the first stage for reuse
* **--prefix=/install** – Installs dependencies into a temporary directory
* **Stage 2 (Runtime)** – Lightweight final image without build tools
* **COPY --from=builder** – Copies only required dependencies
* **Smaller Image** – Build tools are excluded from final image
* **More Secure** – Reduced attack surface



