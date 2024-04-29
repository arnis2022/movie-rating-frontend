# Use node image as base for building
FROM node:lts-alpine AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json .
COPY package-lock.json .
COPY tsconfig.json .
COPY tsconfig.node.json .
COPY vite.config.ts .

# Install dependencies
RUN npm install

# Copy source files
COPY . .

# Build the application for production
RUN npm run build

# Stage 2: Serve the application
FROM nginx:alpine

# Copy built artifacts from the build stage to nginx web server directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 
EXPOSE 3000

# Command to start nginx
CMD ["nginx", "-g", "daemon off;"]
