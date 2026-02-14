# 🐳 MicroTodoUI - Dockerized Frontend Application

## 📌 Overview

This project demonstrates how to Dockerize a frontend application using:

- Node.js (for building the application)
- Nginx (for serving static build files)
- Custom Nginx configuration for SPA routing support

The application is built using Node and served via Nginx inside a container.

---

## 🏗 Architecture

### Build Phase
- Install dependencies using `npm install`
- Generate production build using `npm run build`
- Static files generated inside `/build`

### Serve Phase
- Nginx serves static files from:
  
  ```
  /usr/share/nginx/html
  ```

- Custom Nginx configuration ensures:
  - Static file serving
  - SPA routing support
  - No default 404 behavior

---

## 📂 Project Structure

```
MicroTodoUI/
│
├── public/
├── src/
├── package.json
├── package-lock.json
├── Dockerfile
├── nginx.conf
└── README.md
```

---

## 🐳 Dockerfile Explanation

### 1️⃣ Base Image

```dockerfile
FROM node:16.20.0-alpine
```

Lightweight Alpine-based Node image.

---

### 2️⃣ Install Nginx

```dockerfile
RUN apk add nginx
```

Installs Nginx inside the container.

---

### 3️⃣ Set Working Directory

```dockerfile
WORKDIR /TodoUi
```

Sets working directory inside container.

---

### 4️⃣ Install Dependencies

```dockerfile
COPY package*.json ./
RUN npm install
```

Uses Docker layer caching for faster rebuilds.

---

### 5️⃣ Build Application

```dockerfile
COPY . .
RUN npm run build
```

Creates optimized production build.

---

### 6️⃣ Copy Build Files to Nginx Root

```dockerfile
RUN rm -rf /usr/share/nginx/html/*
RUN cp -r build/. /usr/share/nginx/html/
```

Removes default content and copies built static files.

---

### 7️⃣ Replace Default Nginx Configuration

Alpine Nginx default config returns 404 for all requests.

So we replace it:

```dockerfile
RUN rm -f /etc/nginx/http.d/default.conf
COPY nginx.conf /etc/nginx/http.d/default.conf
```

---

## 🌐 Nginx Configuration (nginx.conf)

```nginx
server {
    listen 80;

    location / {
        root /usr/share/nginx/html;
        index index.html;
        try_files $uri /index.html;
    }
}
```

### Why `try_files` is needed?

For Single Page Applications (React, etc.), refreshing routes like:

```
/dashboard
```

would cause 404 without fallback.

`try_files` ensures all routes fallback to `index.html`.

---

## 🚀 How to Build and Run

### 🔹 Build Docker Image

```bash
docker build -t todoui .
```

---

### 🔹 Run Container

```bash
docker run -d -p 8080:80 --name todoui-container todoui
```

---

### 🔹 Access Application

Open in browser:

```
http://localhost:8080
```

---

## 🛠 Debugging Guide

### Check Running Containers

```bash
docker ps
```

---

### View Logs

```bash
docker logs todoui-container
```

---

### Enter Container

```bash
docker exec -it todoui-container sh
```

---

### Verify Static Files

```bash
ls -la /usr/share/nginx/html
```

---

## ⚠ Common Issues

### 404 Not Found

Possible Causes:

- Default Nginx config returning 404
- Wrong root directory
- Missing `try_files`
- Build files not copied correctly

Solution:

- Ensure custom nginx.conf is copied
- Verify files exist in `/usr/share/nginx/html`
- Rebuild image after changes

---

## 🔁 Rebuild Workflow

```bash
docker build -t todoui .
docker rm -f todoui-container
docker run -d -p 8080:80 --name todoui-container todoui
```

---

## 📚 Key Concepts Learned

- Docker Image vs Container
- RUN vs CMD difference
- Nginx default behavior in Alpine
- Why default config returns 404
- SPA routing using `try_files`
- Importance of reproducible configuration
- Why manual container edits are not recommended

---

## 🚀 Future Improvements

Recommended upgrade:

Use Multi-Stage Build:

- Stage 1 → Build with Node
- Stage 2 → Serve with official `nginx:alpine`

Benefits:

- Smaller image size
- Cleaner architecture
- Production-ready approach

---

## 🧠 Final Note

Always modify Dockerfile or configuration files instead of editing inside a running container.

Containers are ephemeral.  
Images are the source of truth.

```
Infrastructure should be reproducible, not manually patched.
```

---
