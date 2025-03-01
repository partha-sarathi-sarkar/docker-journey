# Stage 1 - Build Stage
FROM node:18 AS builder

WORKDIR /app

# Install Angular CLI globally (optional if you want to build locally first)
RUN npm install -g @angular/cli

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the entire project to container
COPY . .

# Build the Angular application
RUN npm run build --configuration=production

# Stage 2 - Runtime Stage
FROM nginx:alpine

# Copy compiled app to nginx html folder
COPY --from=builder /app/dist/angular-app /usr/share/nginx/html

# Copy custom nginx config
#COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]