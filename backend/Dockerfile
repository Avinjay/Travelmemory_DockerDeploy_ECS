# Use Node.js 22 as the base image
FROM node:22-slim

# Set working directory inside the container
WORKDIR /app

# Copy the rest of your application code
COPY package*.json .
RUN npm install
COPY . .

# Expose the port your app uses
EXPOSE 3001

# Start the app
CMD ["node", "index.js"]
