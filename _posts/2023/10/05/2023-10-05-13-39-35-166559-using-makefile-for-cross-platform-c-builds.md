---
layout: post
title: "Using Makefile for cross-platform C++ builds"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working on C++ projects, it's essential to have a build system in place that can automate the process of compiling and linking the code. A popular choice for many developers is to use a Makefile, which allows for easy management of dependencies and builds across different platforms.

## What is a Makefile?

A Makefile is a simple text file that contains a set of rules defining how to build and compile a project. It consists of a series of target rules, each specifying a set of dependencies and the commands needed to build the target.

Makefiles are commonly used in UNIX-based systems, but they can also be utilized in other platforms, such as Windows using tools like MinGW or Cygwin.

## Writing a Makefile for C++ projects

Here's an example of a Makefile for a cross-platform C++ project:

```make
# Compiler and flags
CXX := g++
CXXFLAGS := -std=c++11 -Wall -Wextra

# Source files and output name
SRCS := main.cpp utils.cpp
TARGET := myprogram

# Object files
OBJS := $(SRCS:.cpp=.o)

# Build target
$(TARGET): $(OBJS)
	$(CXX) $(CXXFLAGS) -o $@ $^

# Compile source files
.cpp.o:
	$(CXX) $(CXXFLAGS) -c $< -o $@

# Clean build artifacts
clean:
	rm -f $(OBJS) $(TARGET)
```

Let's break down the Makefile:

- `CXX` defines the compiler to be used. Here, we are using g++.
- `CXXFLAGS` sets the compiler flags, like enabling C++11 features and displaying additional warnings.
- `SRCS` lists all the source files in your project.
- `TARGET` specifies the name of the output executable.
- `OBJS` contains the object files generated from the source files. It transforms `.cpp` extension to `.o`.
- The target rule `$(TARGET)` specifies the dependencies and commands to build the final executable. It compiles each source file and links them together.
- The rule `.cpp.o` defines how to compile each individual source file into an object file.
- `clean` is a target that removes the build artifacts when we execute `make clean`.

## Building the project

To build the project, open a terminal, navigate to the project directory, and run the `make` command. The Makefile will be read, and the necessary dependencies will be checked and compiled.

```bash
$ make
```

To clean up the build artifacts, you can run:

```bash
$ make clean
```

## Conclusion

Makefiles are a versatile and powerful tool for managing and automating C++ builds. They allow developers to easily specify dependencies and build processes, making it easier to develop and maintain cross-platform projects.

By utilizing a Makefile, you can streamline and automate the build process, saving time and ensuring consistency across different development environments.