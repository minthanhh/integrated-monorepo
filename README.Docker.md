### Building and running your application

When you're ready, start your application by running:
`docker compose up --build`.

Your application will be available at http://localhost:32000.

### Deploying your application to the cloud

First, build your image, e.g.: `docker build -t myapp .`.
If your cloud uses a different CPU architecture than your development
machine (e.g., you are on a Mac M1 and your cloud provider is amd64),
you'll want to build the image for that platform, e.g.:
`docker build --platform=linux/amd64 -t myapp .`.

Then, push it to your registry, e.g. `docker push myregistry.com/myapp`.

Consult Docker's [getting started](https://docs.docker.com/go/get-started-sharing/)
docs for more detail on building and pushing.

### References

- [Docker's Node.js guide](https://docs.docker.com/language/nodejs/)

# syntax=docker/dockerfile:1

# Comments are provided throughout this file to help you get started.

# If you need more help, visit the Dockerfile reference guide at

# https://docs.docker.com/go/dockerfile-reference/

# Want to help us make this template better? Share your feedback here: https://forms.gle/ybq9Krt8jtBL3iCk7

# ARG NODE_VERSION=21.0.0

# ARG PNPM_VERSION=8.15.3

# FROM node:${NODE_VERSION}-alpine

# # Use production node environment by default.

# ENV NODE_ENV production

# # Install pnpm.

# RUN --mount=type=cache,target=/root/.npm \

# npm install -g pnpm@${PNPM_VERSION}

# WORKDIR /usr/src/app

# # Download dependencies as a separate step to take advantage of Docker's caching.

# # Leverage a cache mount to /root/.local/share/pnpm/store to speed up subsequent builds.

# # Leverage a bind mounts to package.json and pnpm-lock.yaml to avoid having to copy them into

# # into this layer.

# RUN --mount=type=bind,source=package.json,target=package.json \

# --mount=type=bind,source=pnpm-lock.yaml,target=pnpm-lock.yaml \

# --mount=type=cache,target=/root/.local/share/pnpm/store \

# pnpm install --prod --frozen-lockfile

# # Run the application as a non-root user.

# USER node

# # Copy the rest of the source files into the image.

# COPY . .

# # Expose the port that the application listens on.

# EXPOSE 32000

# # Run the application.

# CMD .
