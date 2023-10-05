---
layout: post
title: "Using CMake for C++ project organization and structure"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

CMake is a popular build system generator that allows you to organize and structure your C++ projects in a clean and scalable manner. It provides a high-level scripting language (CMakeLists.txt) to define the build process, dependencies, and other project configurations. In this blog post, we will explore how to effectively use CMake to organize and structure your C++ projects.

## Table of Contents

- [What is CMake?](#what-is-cmake)
- [Installing CMake](#installing-cmake)
- [Creating a Simple Project](#creating-a-simple-project)
- [Organizing Project Structure](#organizing-project-structure)
- [Adding External Dependencies](#adding-external-dependencies)
- [Conclusion](#conclusion)

## What is CMake? {#what-is-cmake}

CMake is an open-source build system generator developed by Kitware. It allows developers to define and configure the build process for their projects across different platforms and compilers. CMake generates platform-specific build files (e.g., Makefiles or Visual Studio solutions) based on the project's CMakeLists.txt file.

With CMake, you can easily manage complex build dependencies, organize your project structure, and automate the build process.

## Installing CMake {#installing-cmake}

Before we dig into project organization and structure, let's quickly go over the installation steps for CMake.

1. Visit the CMake download page on the official website: [https://cmake.org/download/](https://cmake.org/download/)
2. Select the appropriate installer for your operating system and download it.
3. Run the installer and follow the instructions to complete the installation.

Once installed, you should have the `cmake` command available in your system's PATH.

## Creating a Simple Project {#creating-a-simple-project}

Let's start by creating a simple C++ project using CMake. Create a new directory for your project and navigate into it.

1. Create a file named `CMakeLists.txt` in the root directory of your project.
2. Open the `CMakeLists.txt` file and add the following minimal configuration:

```cmake
cmake_minimum_required(VERSION 3.15)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)

add_executable(MyProject main.cpp)
```

In the above example, we set the minimum required CMake version, specify the project name, and set the C++ standard to 17. Finally, we define an executable target named `MyProject` with a source file `main.cpp`.

To create the build files, open a terminal, navigate to your project's root directory, and run the following command:

```bash
cmake .
```

This will generate build files according to your `CMakeLists.txt` configuration.

## Organizing Project Structure {#organizing-project-structure}

CMake provides various mechanisms to organize your project structure. You can use directories to logically group source files and separate targets. Let's see an example of how to organize a project with multiple source files.

1. Create the following directory structure:

```
MyProject/
├── CMakeLists.txt
├── src
│   ├── main.cpp
│   ├── utils.cpp
│   └── utils.h
```

2. Update your `CMakeLists.txt` file as follows:

```cmake
cmake_minimum_required(VERSION 3.15)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)

add_executable(MyProject
    src/main.cpp
    src/utils.cpp
    src/utils.h
)
```

In the updated `CMakeLists.txt`, we specify the paths to our source files by listing them relative to the root directory. This allows CMake to correctly compile and link our project.

## Adding External Dependencies {#adding-external-dependencies}

CMake also simplifies the process of adding external dependencies to your project. You can use package managers like Conan or vcpkg, or manually configure the dependencies.

Here's an example of how to add an external dependency using Conan:

1. Install Conan package manager by following the instructions on: [https://conan.io/](https://conan.io/)
2. Open a terminal and navigate to your project's root directory.
3. Run the following command to create a Conan profile for your project:

```bash
conan profile new default --detect
```

4. Edit the `CMakeLists.txt` file to include your dependencies. For example, to add the Boost library:

```cmake
cmake_minimum_required(VERSION 3.15)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)

# Find required Boost components
find_package(Boost 1.70 REQUIRED COMPONENTS system filesystem)

add_executable(MyProject
    src/main.cpp
    src/utils.cpp
    src/utils.h
)

target_link_libraries(MyProject
    PRIVATE Boost::system
    PRIVATE Boost::filesystem
)
```

In the above example, we use `find_package` to locate the required Boost components and then link them to our executable target using `target_link_libraries`.

## Conclusion {#conclusion}

CMake is a powerful build system generator that allows you to organize and structure your C++ projects effectively. It provides flexibility in managing project dependencies, organizing project structure, and automating the build process. By following the steps outlined in this blog post, you can start utilizing CMake to improve your C++ project organization and structure.

#programming #CMake