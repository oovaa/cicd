# CI/CD Pipeline Projects

[![CI/CD](https://img.shields.io/badge/CI%2FCD-Pipeline-blue?style=for-the-badge&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Java](https://img.shields.io/badge/java-Spring%20Boot-red.svg)]()

> **Continuous Integration & Deployment** — Hands-on CI/CD pipeline projects with Spring Boot, GitHub Actions, and Docker.

---

## 🎯 Overview

Practical CI/CD pipeline projects demonstrating modern DevOps practices: automated testing, building, containerization, and deployment using GitHub Actions and Docker.

---

## 📁 Projects

| Project | Description | Tech Stack |
|---------|-------------|------------|
| [`cicd/practice-activity-app`](cicd/practice-activity-app) | Spring Boot app with CI pipeline | Java, Spring Boot, Maven, GitHub Actions |
| [`cicd/coursera-spring-hello-world`](cicd/coursera-spring-hello-world) | Hello World Spring Boot with CI | Java, Spring Boot, GitHub Actions |
| [`cicd/cumulative-task`](cicd/cumulative-task) | Comprehensive CI/CD task | Docker, GitHub Actions, Multi-stage builds |

---

## 🛠 Tech Stack

| Category | Technologies |
|----------|--------------|
| **Language** | Java 17+ |
| **Framework** | Spring Boot 3.x |
| **Build** | Maven 3.8+ |
| **CI/CD** | GitHub Actions |
| **Containerization** | Docker, Docker Compose |
| **Registry** | GitHub Container Registry (GHCR) |

---

## 🚀 Quick Start

```bash
git clone https://github.com/oovaa/cicd.git
cd cicd

# Each project is independent
cd practice-activity-app
./mvnw clean test
```

---

## 🔧 CI/CD Pipeline Features

| Pipeline Stage | Implementation |
|----------------|----------------|
| **Source** | GitHub push/PR triggers |
| **Build** | `mvn clean package` |
| **Test** | Unit + integration tests |
| **Security** | Dependency scanning (Dependabot) |
| **Containerize** | Multi-stage Dockerfile |
| **Push** | GHCR / Docker Hub |
| **Deploy** | Staging/Production environments |

---

## 📋 GitHub Actions Workflow Example

```yaml
# .github/workflows/ci.yml
name: CI Pipeline
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with: { java-version: '17', distribution: 'temurin' }
      - run: ./mvnw clean test
      - uses: docker/build-push-action@v5
        if: github.ref == 'refs/heads/main'
        with: { push: true, tags: ghcr.io/oovaa/app:latest }
```

---

## 📚 Learning Outcomes

- ✅ GitHub Actions workflow syntax
- ✅ Multi-stage Docker builds for Java
- ✅ Maven build lifecycle
- ✅ Test automation in CI
- ✅ Docker layer caching optimization
- ✅ Security scanning in pipeline
- ✅ Artifact publishing to registries
- ✅ Environment promotion strategies

---

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 👤 Author

**Omar Abdulrahim**  
GitHub: [@oovaa](https://github.com/oovaa)  
ALX Software Engineering Program