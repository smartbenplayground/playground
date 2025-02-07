# https://medium.com/@ardasugur/angular-17-ssr-dockerization-fb653b4130c6
# Running Angular:SSR in Docker
FROM node:22-alpine as build

# Set the working directory.
WORKDIR /app/src

# Copy the package json over.
COPY package*.json ./

# similar to npm install, except it's meant to be used in automated environments
# https://docs.npmjs.com/cli/v9/commands/npm-ci
#RUN npm ci

# default npm install
RUN npm install -g npm@latest serve
RUN npm install --force #--production

# Copy all files to root of WorkDir
COPY . ./

# Run the build - runs the ng build
RUN npm run build

FROM node:20.13.1-alpine3.19

# Set the working directory.
WORKDIR /usr/app

# Copy the build output to this machine
COPY --from=build /app/src/dist/my-ssr-app/ ./

# Start the server.js file
CMD node server/server.mjs

# Expose to 8080 for google cloud.
EXPOSE 8080
