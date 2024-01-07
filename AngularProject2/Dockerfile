# Use an official Node.js runtime as a base image
FROM node:21-alpine AS node

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY . .

# Install dependencies
RUN npm install

# Build the Angular app
RUN npm run build

# Use a smaller base image for the production environment
FROM nginx:alpine

# Remove the default Nginx configuration
RUN rm /etc/nginx/conf.d/default.conf

# Copy the custom Nginx configuration
COPY nginx-custom.conf /etc/nginx/conf.d/default.conf

# Copy the built Angular app from the builder stage to the httpd directory
COPY --from=node /app/dist/angular-project2/browser /usr/share/nginx/html
