# Single stage Dockerfile for Todo Frontend

FROM node:16.20.0-alpine

# Install nginx
RUN apk add --no-cache nginx

# Set working directory
WORKDIR /TodoUi

# Copy dependency files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build production files
RUN npm run build

# Remove default nginx config
RUN rm -f /etc/nginx/http.d/default.conf

# Copy custom nginx config
COPY nginx.conf /etc/nginx/http.d/default.conf

# Clear default nginx html directory
RUN rm -rf /usr/share/nginx/html/*

# Copy build files to nginx root
RUN cp -r build/. /usr/share/nginx/html/

# Start nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
