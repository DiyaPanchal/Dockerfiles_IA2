# Dockerfiles_IA2
This repository contains the dockerfiles needed for building a three-tier application in Docker

# Docker File (client)
FROM node:16
This line specifies the base image for the Docker container. In this case, it's using the official Node.js version 16 image as the starting point for building the client tier container.

WORKDIR /app
This line sets the working directory within the container to /app. Any subsequent commands will be executed relative to this directory.

COPY package*.json ./
This line copies the package.json and package-lock.json files from the host machine (the directory where the Dockerfile is located) to the /app directory inside the container. These files are necessary for installing dependencies with npm.

RUN npm install --production
This line runs npm install --production inside the container. It installs the dependencies listed in package.json, excluding those listed under the devDependencies section. The --production flag ensures that only production dependencies are installed, omitting any packages intended for development purposes.

COPY . .
This line copies the rest of the application code from the host machine to the /app directory inside the container. This includes all files and directories present in the same directory as the Dockerfile.

EXPOSE 5000
This line exposes port 5000 on the Docker container. It informs Docker that the container will listen on port 5000 at runtime, allowing external connections to reach the client tier application.

CMD ["npm", "start"]
This line specifies the default command to run when the container starts. In this case, it runs npm start, assuming that this script is defined in the package.json file and is responsible for starting the client tier application.

These lines collectively define the steps required to build a Docker image for the client tier in a multi-container setup. This Docker image can then be deployed as part of a larger application stack using Docker Compose or other orchestration tools.

# Docker File (server)
FROM node:16
This line specifies the base image for the Docker container. In this case, it's using the official Node.js version 16 image as the starting point for building the server tier container.

WORKDIR /app
This line sets the working directory within the container to /app. Any subsequent commands will be executed relative to this directory.

COPY package*.json ./
This line copies the package.json and package-lock.json files from the host machine (the directory where the Dockerfile is located) to the /app directory inside the container. These files are necessary for installing dependencies with npm.

RUN npm install
This line runs npm install inside the container. It installs all dependencies listed in package.json, including both regular dependencies and development dependencies (if any).

COPY . .
This line copies the rest of the application code from the host machine to the /app directory inside the container. This includes all files and directories present in the same directory as the Dockerfile.

EXPOSE 5000
This line exposes port 5000 on the Docker container. It informs Docker that the container will listen on port 5000 at runtime, allowing external connections to reach the server tier application.

CMD ["npm", "start"]
This line specifies the default command to run when the container starts. In this case, it runs npm start, assuming that this script is defined in the package.json file and is responsible for starting the server tier application.

These lines collectively define the steps required to build a Docker image for the server tier in a multi-container setup. This Docker image can then be deployed as part of a larger application stack using Docker Compose or other orchestration tools.
