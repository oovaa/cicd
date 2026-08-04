# CI/CD Pipeline Projects

[![CI/CD](https://img.shields.io/badge/CI%2FCD-Pipeline-blue?style=for-the-badge&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

> **Continuous Integration & Deployment** — Hands-on CI/CD pipeline projects demonstrating automated testing, building, containerization, and deployment using GitHub Actions, Docker, and cloud registries.

---

## 🎯 Overview

This repository contains **three independent CI/CD pipeline projects** showcasing different tech stacks and deployment targets. Each project demonstrates modern DevOps practices with GitHub Actions workflows.

---

## 📁 Projects

| Project | Type | Tech Stack | CI/CD Features |
|---------|------|------------|----------------|
| [`coursera-spring-hello-world`](coursera-spring-hello-world) | Spring Boot App | Java 17, Spring Boot 3, Maven, Docker | Build, test, Docker multi-stage build, push to DigitalOcean Container Registry, SSH deploy |
| [`practice-activity-app`](practice-activity-app) | React/Vite App | React 18, TypeScript, Vite, Nginx, Docker | Build, Docker multi-stage build (Nginx), containerization |
| [`cumulative-task`](cumulative-task) | Node.js/Express App | Node.js, Express, Docker | Build, Docker containerization |

---

## 🛠 Tech Stack (Per Project)

### coursera-spring-hello-world
| Category | Technologies |
|----------|--------------|
| **Language** | Java 17 |
| **Framework** | Spring Boot 3.x |
| **Build** | Maven 3.8+ (wrapper included) |
| **Containerization** | Docker multi-stage build |
| **Registry** | DigitalOcean Container Registry |
| **Deployment** | SSH to remote server |

### practice-activity-app
| Category | Technologies |
|----------|--------------|
| **Language** | TypeScript |
| **Framework** | React 18 + Vite |
| **Web Server** | Nginx (in Docker) |
| **Containerization** | Docker multi-stage build |

### cumulative-task
| Category | Technologies |
|----------|--------------|
| **Language** | JavaScript (Node.js) |
| **Framework** | Express.js |
| **Containerization** | Docker |

---

## 🚀 Quick Start

```bash
git clone https://github.com/oovaa/cicd.git
cd cicd

# Each project is independent - navigate to project directory
cd coursera-spring-hello-world
./mvnw clean test

# Or build Docker image
docker build -t coursera-spring-hello-world .
```

---

## 🔧 GitHub Actions Workflow

The main workflow (`.github/workflows/pipeline.yaml`) demonstrates a complete CI/CD pipeline for the Spring Boot project:

```yaml
# .github/workflows/pipeline.yaml
name: CI/CD Pipeline

on: 
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    environment: DOCR

    steps:
      - name: Check out code
        uses: actions/checkout@v4
      
      - name: Build and Test
        working-directory: ./coursera-spring-hello-world
        run: docker compose up -d

      - name: Login to DigitalOcean Container Registry
        uses: docker/login-action@v3
        with:
          registry: registry.digitalocean.com
          username: ${{ secrets.DIGITALOCEAN_USERNAME }}
          password: ${{ secrets.DIGITALOCEAN_ACCESS_TOKEN }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: ./coursera-spring-hello-world
          push: true
          tags: registry.digitalocean.com/oovaa/cicd:latest 

      - name: Deploy via SSH
        uses: appleboy/ssh-action@v1
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          port: ${{ secrets.PORT }}
          script: |
            docker ps
            docker rm -f ciii | true
            docker pull registry.digitalocean.com/oovaa/cicd
            docker run -d -p 8989:80 --name ciii registry.digitalocean.com/oovaa/cicd:latest         
```

### Pipeline Stages

| Stage | Implementation |
|-------|----------------|
| **Source** | GitHub push to `main` / manual dispatch |
| **Build** | `docker compose up -d` (Spring Boot) |
| **Containerize** | Multi-stage Dockerfile |
| **Registry Login** | DigitalOcean Container Registry |
| **Push** | `docker/build-push-action@v5` to DOCR |
| **Deploy** | SSH to remote server, pull & run container |

---

## 📋 Required Secrets (GitHub)

For the workflow to run, configure these secrets in GitHub repository settings:

| Secret | Description |
|--------|-------------|
| `DIGITALOCEAN_USERNAME` | DigitalOcean registry username |
| `DIGITALOCEAN_ACCESS_TOKEN` | DigitalOcean API token |
| `HOST` | SSH host for deployment |
| `USERNAME` | SSH username |
| `SSH_PRIVATE_KEY` | Private key for SSH |
| `PORT` | SSH port |

---

## 📚 Learning Outcomes

- ✅ GitHub Actions workflow syntax (triggers, jobs, steps, environments)
- ✅ Multi-stage Docker builds for different tech stacks (Java, Node.js, React)
- ✅ Maven build lifecycle & wrapper usage
- ✅ Docker layer caching optimization
- ✅ Container registry authentication (DigitalOcean)
- ✅ SSH-based deployment with `appleboy/ssh-action`
- ✅ Environment-specific secrets management
- ✅ Production deployment patterns (container restart, port mapping)

---

## 📂 Repository Structure

```
cicd/
├── .github/
│   └── workflows/
│       └── pipeline.yaml          # Main CI/CD workflow
├── coursera-spring-hello-world/   # Spring Boot + Maven + Docker
│   ├── src/
│   ├── pom.xml
│   ├── mvnw / mvnw.cmd
│   ├── Dockerfile
│   ├── docker-compose.yaml
│   └── README.md
├── practice-activity-app/         # React + Vite + Nginx + Docker
│   ├── src/
│   ├── public/
│   ├── package.json
│   ├── vite.config.js
│   ├── Dockerfile
│   ├── docker-compose.yml
│   ├── nginx.conf
│   └── README.md
├── cumulative-task/               # Node.js + Express + Docker
│   ├── routes/
│   ├── public/
│   ├── app.js
│   ├── package.json
│   └── README
├── post.md                        # Additional notes
├── script.sh                      # Utility script
└── README.md
```

---

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 👤 Author

**Omar Abdulrahim**  
GitHub: [@oovaa](https://github.com/oovaa)  
ALX Software Engineering Program