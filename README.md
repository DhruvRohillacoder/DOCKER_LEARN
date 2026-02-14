# 🐳 Docker Learning Repository

<p align="center">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
  <img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge" alt="Status"/>
  <img src="https://img.shields.io/badge/Learning-In%20Progress-blue?style=for-the-badge" alt="Learning"/>
</p>

## 📖 About

This repository is dedicated to my **Docker learning journey**. It contains various Docker-based projects, practical implementations, and hands-on examples to understand containerization concepts and Docker best practices.

Each project demonstrates different aspects of Docker, from basic containerization to advanced deployment strategies with multi-stage builds, Docker Compose, and production-ready configurations.

---

## 🎯 Purpose

- **Learn** Docker fundamentals and advanced concepts
- **Practice** containerizing real-world applications
- **Explore** different Docker configurations and deployment strategies
- **Document** learning progress and solutions
- **Build** a portfolio of Docker-based projects

---

## 📁 Repository Structure

```
DOCKER_LEARN/
├── projects/
│   ├── project1/          # React Todo App with Nginx
│   ├── project2/          # [Coming Soon]
│   └── ...                # More projects will be added
└── README.md
```

---

## 🚀 Projects

### 1. React Todo App with Nginx

**Status:** ✅ Completed

A React-based Todo application containerized using Docker with Nginx as the web server. This project demonstrates:

- Single-stage Docker build process
- Nginx configuration for serving React SPA
- React Router compatibility
- Production-ready deployment

**Tech Stack:** React, Node.js, Nginx, Docker

📂 [View Project](./projects/project1/) | 📝 [Documentation](./projects/project1/README.md)

---

### 2. [Future Project]

**Status:** 🔜 Coming Soon

More Docker projects will be added as I progress through my learning journey.

---

## 🛠️ Technologies & Tools

<p align="left">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
  <img src="https://img.shields.io/badge/Docker%20Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker Compose"/>
  <img src="https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white" alt="Nginx"/>
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" alt="Node.js"/>
  <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React"/>
  <img src="https://img.shields.io/badge/Alpine%20Linux-0D597F?style=for-the-badge&logo=alpine-linux&logoColor=white" alt="Alpine Linux"/>
</p>

---

## 📚 What You'll Learn

Through the projects in this repository, you'll explore:

- ✅ Docker basics (images, containers, volumes, networks)
- ✅ Writing efficient Dockerfiles
- ✅ Single-stage and multi-stage builds
- ✅ Container orchestration basics
- ✅ Nginx configuration for web apps
- ✅ Deploying containerized applications
- 🔜 Docker Compose for multi-container apps
- 🔜 Docker volumes and data persistence
- 🔜 Container networking
- 🔜 Docker security best practices
- 🔜 CI/CD with Docker
- 🔜 Production deployment strategies

---

## 🏁 Getting Started

### Prerequisites

Before running any project, ensure you have:

- **Docker** installed on your machine
  - [Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/)
  - [Docker Desktop for Mac](https://docs.docker.com/desktop/install/mac-install/)
  - [Docker Engine for Linux](https://docs.docker.com/engine/install/)

### Verify Installation

```bash
docker --version
docker compose version
```

### Running a Project

Navigate to any project directory and follow its specific README instructions. Generally:

```bash
# Clone the repository
git clone https://github.com/DhruvRohillacoder/DOCKER_LEARN.git

# Navigate to a project
cd DOCKER_LEARN/projects/project1

# Build and run
docker build -t project-name .
docker run -p 8080:80 project-name
```

---

## 📖 Useful Docker Commands

### Image Management

```bash
# List all images
docker images

# Remove an image
docker rmi <image_name>

# Remove all unused images
docker image prune -a
```

### Container Management

```bash
# List running containers
docker ps

# List all containers
docker ps -a

# Stop a container
docker stop <container_id>

# Remove a container
docker rm <container_id>

# Remove all stopped containers
docker container prune
```

### Logs & Debugging

```bash
# View container logs
docker logs <container_id>

# Follow logs in real-time
docker logs -f <container_id>

# Execute command in running container
docker exec -it <container_id> /bin/sh
```

### System Cleanup

```bash
# Remove all unused containers, networks, images
docker system prune

# Remove everything including volumes
docker system prune -a --volumes
```

---

## 📝 Best Practices Followed

- ✅ Use official base images
- ✅ Keep images small (Alpine Linux)
- ✅ Multi-stage builds for optimization
- ✅ Proper .dockerignore files
- ✅ Layer caching optimization
- ✅ Security best practices
- ✅ Clear documentation
- ✅ Environment-specific configurations

---

## 🎓 Learning Resources

- [Official Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

---

## 🤝 Contributing

This is a personal learning repository, but suggestions and improvements are welcome! Feel free to:

- Open an issue for suggestions
- Submit a pull request with improvements
- Share your feedback

---

## 📫 Connect With Me

- **GitHub:** [@DhruvRohillacoder](https://github.com/DhruvRohillacoder)
- **Repository:** [DOCKER_LEARN](https://github.com/DhruvRohillacoder/DOCKER_LEARN)

---

## 📄 License

This project is open source and available for learning purposes.

---

## ⭐ Show Your Support

If you find this repository helpful for your Docker learning journey, please consider giving it a star! ⭐

---

<p align="center">
  <b>🚀 Happy Learning! 🐳</b>
</p>

---

