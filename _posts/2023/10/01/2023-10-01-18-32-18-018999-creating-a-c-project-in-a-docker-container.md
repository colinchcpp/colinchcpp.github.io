---
layout: post
title: "Creating a C++ project in a Docker container"
description: " "
date: 2023-10-01
tags: [docker]
comments: true
share: true
---

In this tutorial, we will learn how to set up a development environment for a C++ project using Docker. Docker provides a way to encapsulate dependencies and create portable development environments, making it easier to share and collaborate on projects.

## Prerequisites

Before we get started, make sure you have Docker installed on your machine. You can download and install Docker from the official website: [https://www.docker.com/](https://www.docker.com/)

## Step 1: Create a Dockerfile

The Dockerfile is a text file that contains instructions to build a Docker image. Let's create a new file called `Dockerfile` in the root directory of your project and add the following content:

```dockerfile
# Use the official gcc image as the base image
FROM gcc:latest

# Set the working directory to /app
WORKDIR /app

# Copy the contents of the current directory to /app
COPY . /app

# Compile the C++ code
RUN g++ -o myapp main.cpp

# Set the command to run the application
CMD ["./myapp"]
```

In this Dockerfile, we start with the official GCC (GNU Compiler Collection) image as the base image. We then set the working directory to `/app` and copy the contents of the current directory to `/app` in the container. Next, we compile our C++ code using the `g++` compiler, and finally, we set the command to run our application.

## Step 2: Build the Docker Image

To build the Docker image, open your terminal or command prompt, navigate to the project directory, and run the following command:

```bash
docker build -t my-cpp-app .
```

This command tells Docker to build an image based on the `Dockerfile` in the current directory and name it `my-cpp-app`.

## Step 3: Run the Docker Container

Once the image is built, we can create and run a Docker container based on that image. Run the following command:

```bash
docker run my-cpp-app
```

This command starts a new Docker container based on the `my-cpp-app` image. It will compile and run the C++ code inside the container.

That's it! You have successfully set up a development environment for your C++ project using Docker. Now you can easily share the Docker image with others, ensuring consistent and reproducible builds across different machines.

#cpp #docker