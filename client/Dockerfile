#e an official Node.js runtime as the base image
FROM node:12

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

RUN sudo apt update && apt install vi -y

# Install project dependencies
RUN npm install --progress=false

# Copy the rest of the application code to the container
COPY . .

# Expose port 80
EXPOSE 3000

# Build the React application
RUN npm run build



# Command to run the application
CMD ["npm", "start"]
