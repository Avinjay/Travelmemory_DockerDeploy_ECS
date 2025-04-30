# Use Node.js 22 as the base image for the build stage
FROM node:22-slim as builder

# Set working directory inside the container
WORKDIR /front-app

# Copy package.json and package-lock.json first (to leverage Docker cache for dependencies)
COPY package*.json ./

# Install production dependencies
RUN npm install --only=production

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Production stage: Use a slim Node.js image to serve the app
FROM node:22-slim as production

# Set working directory
WORKDIR /front-app

# Install 'serve' to serve the built app
RUN npm install -g serve

# Copy the built React app from the build stage
COPY --from=builder /front-app/build /front-app/build

# Expose the port the app will run on
EXPOSE 3000

# Start the app using the 'serve' static server
CMD ["serve", "-s", "build", "-l", "3000"]
