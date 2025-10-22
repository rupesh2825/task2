# Use Node.js official image as base
FROM node:18-alpine

# Set working directory
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install --production

# Copy rest of the files
COPY . .

# Expose the app port
EXPOSE 3000

# Command to run the app
CMD ["npm", "start"]
