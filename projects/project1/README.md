# DOCKER_LEARN

This is Repo For My DOCKER Learnings.....

## Project Structure

```
DOCKER_LEARN/
├── projects/
│   ├── project1/          # React Todo App with Nginx
│   │   ├── Dockerfile
│   │   ├── nginx.conf
│   │   ├── package.json
│   │   └── src/
│   └── project2/
└── README.md
```

---

## Project 1: React Todo App with Nginx

### Overview

A React-based Todo application containerized using Docker with Nginx as the web server.

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

### Setup Options

You can run this project in two ways:

1. **Manual Setup** (Without Docker) - Traditional way
2. **Docker Setup** (Recommended) - Containerized approach

---

### Option 1: Manual Setup (Without Docker)

**Prerequisites:**

- NodeJs 16.x
- NPM
- Nginx server (on Ubuntu or your OS)

**Steps:**

1. **Install NodeJs 16.x and NPM on Ubuntu:**

   ```bash
   curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
   sudo apt-get install -y nodejs
   node --version  # Verify installation
   npm --version
   ```

2. **Update the backend URL:**
   - Open `src/TodoApp.js`
   - Update the backend API URL according to your backend server

3. **Install dependencies:**

   ```bash
   npm install
   ```

4. **Build the production app:**

   ```bash
   npm run build
   ```

5. **Copy generated artifacts to nginx server:**

   ```bash
   # The build folder contains production-ready files
   sudo cp -r build/* /usr/share/nginx/html/

   # Or configure nginx to point to your build directory
   ```

6. **Configure Nginx:**
   - Copy the `nginx.conf` to nginx configuration directory
   - Restart nginx: `sudo systemctl restart nginx`

---

### Option 2: Docker Setup (Recommended)

**Why Docker?**

- No need to install NodeJs, NPM, or Nginx on your system
- Consistent environment across all machines
- Easy deployment and scaling
- All dependencies bundled in one container

### Dockerfile Explanation

**Single-stage build process:**

```dockerfile
# Use Node.js Alpine base image (lightweight)
FROM node:16.20.0-alpine

# Install nginx web server
RUN apk add --no-cache nginx

# Set working directory inside container
WORKDIR /TodoUi

# Copy package files
COPY package*.json ./

# Install all dependencies
RUN npm install

# Copy application source code
COPY . .

# Build production-ready React app
RUN npm run build

# Remove default nginx configuration
RUN rm -f /etc/nginx/http.d/default.conf

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/http.d/default.conf

# Clear default nginx HTML directory
RUN rm -rf /usr/share/nginx/html/*

# Copy React build files to nginx serving directory
RUN cp -r build/. /usr/share/nginx/html/

# Start nginx in foreground mode
CMD ["nginx", "-g", "daemon off;"]
```

### Nginx Configuration (nginx.conf)

**Purpose:** Configure nginx to properly serve the React SPA (Single Page Application)

```conf
server {
    # Listen on port 80 (HTTP)
    listen 80;

    location / {
        # Serve files from this directory
        root /usr/share/nginx/html;

        # Default file to serve
        index index.html;

        # Important for React Router
        # If file doesn't exist, serve index.html
        # This enables client-side routing to work
        try_files $uri /index.html;
    }
}
```

**Key Concepts:**

1. **`listen 80`**: Nginx listens on port 80 for incoming HTTP requests

2. **`root /usr/share/nginx/html`**: Directory where React build files are stored

3. **`index index.html`**: Default file to serve when accessing root URL

4. **`try_files $uri /index.html`**:
   - First tries to serve the requested file (`$uri`)
   - If file doesn't exist, serves `index.html` instead
   - **Why?** React Router handles routing on client-side
   - Without this, refreshing pages like `/dashboard` would show 404

### How to Build and Run with Docker

```bash
# Navigate to project directory
cd projects/project1

# Build Docker image
docker build -t todo-app .

# Run container (map container port 80 to host port 8080)
docker run -p 8080:80 todo-app

# Access application
# Open browser: http://localhost:8080
```

### Local Development (Without Docker)

For development purposes, you can run the app locally:

```bash
# Navigate to project directory
cd projects/project1

# Install dependencies
npm install

# Start development server
npm start

# App will open at http://localhost:3000
```

**Development vs Production:**

- `npm start` - Development mode with hot reload
- `npm run build` - Production build (optimized and minified)
- Docker uses production build for better performance

### Common Docker Commands

```bash
# List all images
docker images

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Stop container
docker stop <container_id>

# Remove container
docker rm <container_id>

# Remove image
docker rmi <image_name>

# View container logs
docker logs <container_id>

# Execute command inside running container
docker exec -it <container_id> /bin/sh
```

---

## Key Learning Points

### 1. **Single-Stage vs Multi-Stage Builds**

- This project uses single-stage build (simple but larger image)
- Multi-stage builds can reduce final image size significantly

### 2. **Why Nginx for React Apps?**

- React builds to static files (HTML, CSS, JS)
- Nginx efficiently serves static content
- Lightweight and fast
- Handles SPA routing properly

### 3. **Port Mapping**

- Container runs nginx on port 80 (internal)
- `-p 8080:80` maps host port 8080 to container port 80
- Access via `localhost:8080` from browser

### 4. **Alpine Linux**

- Minimal Docker base image
- Smaller image size
- Faster builds and deployments
- Uses `apk` package manager instead of `apt`

---

## Future Improvements

- [ ] Implement multi-stage build to reduce image size
- [ ] Add docker-compose for easier container management
- [ ] Add environment variables for configuration
- [ ] Implement CI/CD pipeline
- [ ] Add health checks
- [ ] Use nginx official image for multi-stage build

---

## Resources

- [Docker Documentation](https://docs.docker.com/)
- [Nginx Documentation](https://nginx.org/en/docs/)
- [Docker Hub](https://hub.docker.com/)
