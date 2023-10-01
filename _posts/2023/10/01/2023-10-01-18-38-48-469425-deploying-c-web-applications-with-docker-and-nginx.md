---
layout: post
title: "Deploying C++ web applications with Docker and NGINX"
description: " "
date: 2023-10-01
tags: [docker, webdevelopment]
comments: true
share: true
---

In this blog post, we will explore the process of deploying C++ web applications using Docker and NGINX. Docker allows us to package our application and its dependencies into a container, providing a consistent and portable environment. NGINX, on the other hand, serves as the web server that handles incoming requests and forwards them to our application.

Before we begin, make sure you have Docker and NGINX installed on your machine. Let's get started!

## Step 1: Creating the Dockerfile

First, we need to create a `Dockerfile` in the root directory of our application. This file will define the steps and instructions to build our Docker image.

```dockerfile
# Use a base image with the necessary build tools and libraries
FROM gcc:latest

# Set the working directory
WORKDIR /app

# Copy the source code into the container
COPY . .

# Build the application
RUN g++ -o app main.cpp

# Specify the command to run when the container starts
CMD ["./app"]
```

In the above `Dockerfile`, we start with a base image that has the necessary build tools and libraries for C++ development. We then set the working directory of the container to `/app` and copy the source code into it. Next, we compile our C++ application using `g++` and name the executable `app`. Finally, we specify the command to run when the container starts, which is executing our application.

## Step 2: Building the Docker Image

To build the Docker image, navigate to the root directory of your application in the terminal and run the following command:

```bash
docker build -t myapp .
```

Where `myapp` is the name you want to give to your Docker image. This command will read the `Dockerfile`, execute the instructions, and build the image.

## Step 3: Running the Docker Container

Now that we have our Docker image, we can run it as a container. To expose the container's port and map it to the host, use the following command:

```bash
docker run -d -p 80:80 myapp
```

This command will start the container in detached mode (`-d`) and map port 80 of the host to the container's port 80.

## Step 4: Configuring NGINX

Next, we need to configure NGINX to proxy requests to our C++ application running in the Docker container. Create an NGINX configuration file, e.g., `myapp.conf`, with the following content:

```nginx
server {
    listen 80;
    server_name myapp.com;

    location / {
        proxy_pass http://localhost:80;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

The `listen` directive specifies the port to listen on, and `server_name` defines the domain name or IP address of your application. The `location` block proxies requests to `http://localhost:80`, which corresponds to the Docker container running our C++ application.

## Step 5: Running NGINX with Docker

To run NGINX as a Docker container and use our custom configuration file, execute the following command:

```bash
docker run -p 80:80 -v /path/to/myapp.conf:/etc/nginx/conf.d/default.conf nginx
```

Where `/path/to/myapp.conf` is the path to the configuration file we created. This command starts an NGINX container, maps port 80 of the host to port 80 of the container, and mounts the configuration file inside the container.

## Conclusion

Congratulations! You have successfully deployed your C++ web application using Docker and NGINX. By containerizing our application, we ensure consistent behavior across different environments and ease of deployment. NGINX acts as a reliable and performant web server, allowing us to handle incoming requests with ease.

#docker #cpp #webdevelopment #nginx