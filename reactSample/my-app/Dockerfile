# https://www.googlecloudcommunity.com/gc/Community-Blogs/No-servers-no-problem-A-guide-to-deploying-your-React/ba-p/690760
# Use the official lightweight Node.js 18 image.
# https://hub.docker.com/_/node
FROM node:22-alpine as build

# Create and change to the app directory.
WORKDIR /usr/src/app

# Set the PYTHONPATH environment variable, which is occasionally necessary for certain node packages
# 'PWD' is an environment variable that stores the path of the current working directory
ENV PYTHONPATH=${PYTHONPATH}:${PWD}

# Copy application dependency manifests to the container image.
# A wildcard is used to ensure both package.json AND package-lock.json are copied.
# Copying this separately prevents re-running npm install on every code change.
COPY package*.json ./

# Set the environment variable for the application's port
# (Be sure to replace '8080' with your application's specific port number if different)
ENV PORT 8080

# Install dependencies.
# If you add a package-lock.json speed your build by switching to 'npm ci'.
# RUN npm ci --only=production
RUN npm install -g npm@latest serve
RUN npm install --force #--production

# Copy local code to the container image.
COPY . ./

# Build the React app
RUN npm run build

# Serve the 'build' directory on port 8080 using 'serve'
CMD ["serve", "-s", "-l", "8080", "./build"]