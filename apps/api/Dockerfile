# Build context = monorepo root:
#   docker build -f apps/api/Dockerfile -t key-sell-services .

# Use the official Node.js 22 image as the base image
FROM node:22-slim

# Install dependencies
RUN apt-get update && apt-get install -y wkhtmltopdf curl && rm -rf /var/lib/apt/lists/*

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy the workspace manifests and the root lockfile
COPY package.json package-lock.json ./
COPY apps/api/package.json apps/api/
COPY apps/web/package.json apps/web/

# Install the API dependencies only
RUN npm ci -w @key-sell/api --include-workspace-root

# Copy the API sources
COPY apps/api apps/api

# Build the NestJS application
RUN npm run build -w @key-sell/api

# Expose the application port
EXPOSE 3000

# Command to run the application (cwd stays /usr/src/app, as before the monorepo)
CMD ["node", "apps/api/dist/main"]
