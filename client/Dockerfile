# Use an official Node.js runtime as the base image
FROM node:14 as build

# Set the working directory
WORKDIR /app/client

# Copy package.json and package-lock.json to the working directory
COPY ./client/package*.json ./

# Install dependencies
RUN npm install

# Copy the entire app to the container
COPY ./client ./

# Build the app
RUN npm run build

# Use a smaller base image for the runtime
FROM nginx:alpine

# Copy the built app from the previous stage
COPY --from=build /app/client/build /usr/share/nginx/html

# Expose the port the app runs on
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
