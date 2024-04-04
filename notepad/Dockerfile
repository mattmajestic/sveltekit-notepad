# Use the official Node.js 18 image from Docker Hub
FROM node:18-alpine

# Set the working directory in the Docker container
WORKDIR /app

# Copy the package.json and package-lock.json (or npm-shrinkwrap.json) files
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the rest of the project files into the Docker container
COPY . .

# Expose the port that SvelteKit runs on by default (check if your app uses a different port)
EXPOSE 5173

# Run the SvelteKit development server
CMD ["npm", "run", "dev"]
