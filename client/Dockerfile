#e an official Node.js runtime as the base image
FROM node:13.12.0-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

ENV PATH /app/node_modules/.bin:$PATH

RUN npm install --silent

RUN npm install react-scripts@3.4.1 -g --silent

# Copy the rest of the application code to the container
COPY . .

# Build the React application
RUN npm run build

# Expose port 80
EXPOSE 3000


# Command to run the application
CMD ["npm", "start"]
