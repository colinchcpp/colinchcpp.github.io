---
layout: post
title: "Running and testing C++ applications inside Docker containers"
description: " "
date: 2023-10-01
tags: [Cplusplus, Docker]
comments: true
share: true
---

Docker has become a popular choice for packaging and deploying applications due to its lightweight and portable nature. In this blog post, we will explore how to run and test C++ applications inside Docker containers, providing an isolated and reproducible environment for development and testing.

## Setting Up Docker

Before we can start running and testing our C++ applications inside Docker containers, we need to make sure that Docker is installed and properly set up on our system. Follow the Docker documentation for your specific operating system to install Docker.

## Creating a Docker Image for C++

The next step is to create a Docker image that will serve as the base for our C++ applications. We can start with a base image like `ubuntu` or `debian` and install the necessary development tools such as `g++` and `cmake`.

Here is an example `Dockerfile` for creating a C++ development image:

```dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
  g++ \
  cmake

WORKDIR /app

CMD ["bash"]
```

Save the above `Dockerfile` in a directory of your choice. Open a terminal in that directory and build the Docker image using the following command:

```shell
docker build -t cpp-dev:latest .
```

This command will build the Docker image with a tag name `cpp-dev` and the `latest` version.

## Running C++ Applications in Docker Containers

Now that we have our Docker image ready, we can run our C++ applications inside Docker containers. Let's assume we have a simple hello world C++ program named `hello.cpp`.

To run this program inside a Docker container, we need to mount the source code directory as a volume and set the working directory to that directory inside the container. We also need to specify the Docker image we want to use.

Use the following command to run the program inside a Docker container:

```shell
docker run --rm -v $(pwd):/app -w /app cpp-dev:latest g++ -o hello hello.cpp && ./hello
```

Explanation of the command:

- `--rm`: Removes the container after it exits.
- `-v $(pwd):/app`: Mounts the current directory as a volume inside the container, which makes the source code accessible.
- `-w /app`: Sets the working directory inside the container to the mounted volume.
- `cpp-dev:latest`: Specifies the Docker image to use.
- `g++ -o hello hello.cpp`: Compiles the `hello.cpp` source code and generates an executable named `hello`.
- `./hello`: Runs the compiled executable.

## Testing C++ Applications in Docker Containers

To test our C++ applications inside Docker containers, we can leverage tools like CMake and a testing framework like Google Test.

Let's assume we have a C++ application with its associated unit tests. We can create a `CMakeLists.txt` file to build our application and tests:

```cmake
cmake_minimum_required(VERSION 3.12)
project(myapp)

set(CMAKE_CXX_STANDARD 17)

add_executable(myapp main.cpp)

enable_testing()
add_subdirectory(tests)
```

Inside the `tests` directory, we can have a separate `CMakeLists.txt` file to build and run our tests:

```cmake
add_executable(myapp_tests test1.cpp test2.cpp)
target_link_libraries(myapp_tests gtest_main gtest)

add_test(NAME myapp_tests COMMAND myapp_tests)
```

With the Docker image we created earlier, we can build and run our tests inside a Docker container:

```shell
docker run --rm -v $(pwd):/app -w /app cpp-dev:latest cmake .
docker run --rm -v $(pwd):/app -w /app cpp-dev:latest make
docker run --rm -v $(pwd):/app -w /app cpp-dev:latest ./myapp_tests
```

Once the above commands are executed, the tests will run inside the Docker container, providing an isolated environment to validate the behavior of our C++ application.

## Conclusion

Running and testing C++ applications inside Docker containers offers a convenient and reproducible way to develop and validate our code. Docker provides a lightweight and isolated environment that ensures consistent results across different systems. With the steps outlined in this blog post, you can easily set up and leverage Docker containers for running and testing your C++ applications. Start experimenting and see the benefits it brings to your development workflow.

#Cplusplus #Docker