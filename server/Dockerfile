# Use an official Node.js runtime as the base image
FROM node:14

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the entire app to the container
COPY . .

# Expose the port the server runs on
EXPOSE 4000

# Start the server
CMD ["node", "index.js"]
