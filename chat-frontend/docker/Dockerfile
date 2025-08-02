# Use an official Node.js runtime as a parent image
FROM node:22-slim

ENV DEBIAN_FRONTEND=noninteractive

# Install commonly used CLI tools
RUN apt-get update && apt-get install -y git curl && apt-get clean && rm -rf /var/lib/apt/lists/*

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to leverage Docker layer caching.
#COPY package*.json ./

# Copy the rest of the application's source code.
COPY . .

# Install all project dependencies, including devDependencies.
RUN npm install

# Expose the port the Next.js development server runs on.
EXPOSE 9002

# Start the Next.js development server.
# The "--hostname 0.0.0.0" flag is crucial for making the application
# accessible from outside the container.
CMD ["npm", "run", "dev", "--", "--hostname", "0.0.0.0"]