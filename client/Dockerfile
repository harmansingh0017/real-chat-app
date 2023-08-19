#e an official Node.js runtime as the base image
FROM node:20

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

 

# Install project dependencies
RUN npm install --progress=false

# Copy the rest of the application code to the container
COPY . .

# Expose port 80
EXPOSE 3000


# Command to run the application
CMD ["npm", "start"]
