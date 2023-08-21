#e an official Node.js runtime as the base image
FROM node:16-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

RUN npm install  

# Copy the rest of the application code to the container
COPY . .

# Build the React application
RUN npm run build

# Expose port 80
EXPOSE 3000


# Command to run the application
CMD ["npm", "start"]
