# Stage 1: Base - Install dependencies
FROM node:18 AS base
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Stage 2: Runtime - Copy code and run
FROM node:18-slim

WORKDIR /app

# Copy node_modules from the previous stage
COPY --from=base /app/node_modules ./node_modules

# Copy the application code
COPY src ./src
COPY package.json .

# Expose port
EXPOSE 3000

# Run the application
CMD ["npm", "start"]
