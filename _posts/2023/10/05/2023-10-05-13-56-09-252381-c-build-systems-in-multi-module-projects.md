---
layout: post
title: "C++ Build Systems in multi-module projects"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working on large C++ projects with multiple modules, managing the build system becomes crucial. A build system automates the process of compiling source code, linking libraries, and generating executables. It ensures that only modified files are recompiled and accelerates the development workflow.

In this article, we will explore two popular build systems for C++ projects in the context of multi-module projects: **CMake** and **Bazel**.

## CMake

CMake is a cross-platform build system generator that allows developers to define the build process in a platform-independent manner. It uses CMakeLists.txt files to specify build configurations, dependencies, and target generation.

### Advantages of CMake

- **Cross-platform support**: CMake is designed to work seamlessly across various platforms, including Windows, macOS, and Linux.
- **Modular and scalable**: CMake supports multi-module projects, allowing developers to organize code into separate modules and handle dependencies effectively.
- **Extensible and customizable**: CMake offers numerous built-in features and extensions to customize the build process according to project requirements.
- **Ease of use**: CMake employs a simple syntax that is easy to understand and modify, making it accessible to both beginners and experts.

### Example CMakeLists.txt

Here's an example `CMakeLists.txt` file for a multi-module C++ project:

```cmake
cmake_minimum_required(VERSION 3.12)
project(MyProject)

# Add submodules
add_subdirectory(module1)
add_subdirectory(module2)

# Define executable and its dependencies
add_executable(my_app main.cpp)
target_link_libraries(my_app module1 module2)
```

In this example, the project consists of two modules (`module1` and `module2`), which are added as subdirectories. The `my_app` executable is defined and linked with the modules.

## Bazel

Bazel is an open-source build system developed by Google. It emphasizes scalability, reproducibility, and performance. Bazel builds code based on a directed acyclic graph (DAG) of build targets, which makes it well-suited for large projects with complex dependencies.

### Advantages of Bazel

- **Scalability**: Bazel is designed to handle large codebases efficiently, making it suitable for projects with thousands of source files and complex dependency graphs.
- **Incremental builds**: Bazel employs caching and dependency tracking to ensure that only modified parts of the project are recompiled, leading to faster build times.
- **Reproducibility**: Bazel enforces deterministic builds, ensuring that the same set of inputs will always produce the same output, regardless of the build environment.
- **Support for multiple languages**: Bazel supports not only C++ but also many other programming languages, making it suitable for multi-language projects.

### Example BUILD files

In Bazel, build configurations are defined using `BUILD` files. Here's an example `BUILD` file for a multi-module project:

```python
cc_library(
    name = "module1",
    srcs = ["module1.cpp"],
    hdrs = ["module1.h"],
    deps = [
        ":module2",
    ],
)

cc_library(
    name = "module2",
    srcs = ["module2.cpp"],
    hdrs = ["module2.h"],
)

cc_binary(
    name = "my_app",
    srcs = ["main.cpp"],
    deps = [
        ":module1",
        ":module2",
    ],
)
```

In this example, `cc_library` is used to define the modules (`module1` and `module2`) with their source files, headers, and dependencies. The `cc_binary` rule defines the `my_app` executable, which depends on the two modules.

## Conclusion

Managing the build system in multi-module C++ projects is essential for efficient development. Both CMake and Bazel offer powerful features and flexibility for organizing and building projects with complex dependencies. Choose the one that best suits your project's requirements and start simplifying your build process today.

**#CMake #Bazel**