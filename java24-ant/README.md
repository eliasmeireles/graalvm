# GraalVM Docker Project

## Overview

This project provides a Docker container with:

- GraalVM JDK 24 (community edition)
- Apache Ant 1.10.14 pre-installed
- Optimized for Java development and native image compilation

**Docker Image:** `ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14`

## Quick Start

### Pull the Image

```bash
docker pull ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14
```

### Run Interactive Shell

```bash
docker run -it --rm ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14
```

## Usage Examples

### 1. Basic Java Compilation

```bash
docker run --rm -v $(pwd):/app ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14 \
  javac /app/MyApp.java
```

### 2. Ant Build Project

```bash
docker run --rm -v $(pwd):/app ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14 \
  ant -f /app/build.xml
```

### 3. Create Native Image

```bash
docker run --rm -v $(pwd):/app ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14 \
  native-image -jar /app/target/myapp.jar
```

### 4. Development Environment (Persistent)

```bash
docker run -it --rm \
  -v $(pwd):/app \
  -p 8080:8080 \
  --name graalvm-dev \
  ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14
```

## Common Tools Verification

Verify installed tools work correctly:

```bash
# Check Java version
docker run --rm ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14 java -version

# Check Ant version
docker run --rm ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14 ant -version
```

## Environment Details

| Component   | Version           | Location     |
|-------------|-------------------|--------------|
| GraalVM JDK | 24                | /opt/graalvm |
| Apache Ant  | 1.10.14           | /opt/ant     |
| Java        | GraalVM Community | $JAVA_HOME   |

## Best Practices

1. **Volume Mounting**: Always mount your project directory to `/app` for persistence
2. **Cleanup**: Use `--rm` flag to automatically remove containers after exit
3. **Resource Limits**: For native image compilation, add `--memory=4g` for better performance

## Building Custom Images

Extend this image in your Dockerfile:

```dockerfile
FROM ghcr.io/eliasmeireles/graalvm:jdk24-ant.1.10.14

# Add your customizations
RUN gu install native-image
COPY . /app
```
