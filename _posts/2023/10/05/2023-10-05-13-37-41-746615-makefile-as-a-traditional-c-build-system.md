---
layout: post
title: "Makefile as a traditional C++ Build System"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When it comes to building C++ projects, there are various build systems available, each with its own advantages and disadvantages. One traditional and widely used build system is `make` along with a `Makefile`. In this blog post, we will explore the basics of a `Makefile` and how it can be used as a C++ build system.

## Table of Contents
1. [Introduction to Makefile](#introduction-to-makefile)
2. [The Makefile Structure](#the-makefile-structure)
3. [Defining Targets and Prerequisites](#defining-targets-and-prerequisites)
4. [Using Variables in Makefile](#using-variables-in-makefile)
5. [Compiling C++ Code with Makefile](#compiling-c-code-with-makefile)
6. [Cleaning Up with Phony Targets](#cleaning-up-with-phony-targets)
7. [Conclusion](#conclusion)

## Introduction to Makefile
A `Makefile` is a build configuration file that specifies how to compile and build a project. It contains rules, targets, dependencies, and actions to be executed. The `make` tool reads the `Makefile` and executes the necessary actions based on the file's rules.

## The Makefile Structure
A `Makefile` consists of rules in the following format:

```
target: prerequisites
    rules
```

- **Target**: The file or action to be built or executed.
- **Prerequisites**: The files or actions required to build the target.
- **Rules**: The actions to be executed when building the target.

## Defining Targets and Prerequisites
Targets can be any file or action, such as compiling a C++ file or cleaning up generated files. Prerequisites are the files that the target depends on and must exist or be up to date before executing the rules.

For example, consider a simple `Makefile` that compiles a C++ source file:

```makefile
main: main.cpp
    g++ -o main main.cpp
```

In this example, `main` is the target, `main.cpp` is the prerequisite, and the rule specifies how to compile `main.cpp` using the `g++` compiler.

## Using Variables in Makefile
Variables in `Makefile` can be used to store values and make the build rules more flexible. They are defined using the format `variable_name = value`. To use a variable, prefix it with the `$` symbol.

```makefile
CXX = g++
CXXFLAGS = -std=c++17 -Wall

main: main.cpp
    $(CXX) $(CXXFLAGS) -o main main.cpp
```

In this example, the `CXX` variable stores the compiler (`g++`), and `CXXFLAGS` stores the compiler flags (`-std=c++17 -Wall`). These variables are then used in the rule to compile the C++ file.

## Compiling C++ Code with Makefile
To compile multiple files or when dependencies are involved, Makefile can become more complex. Let's consider a scenario with multiple source files:

```makefile
CXX = g++
CXXFLAGS = -std=c++17 -Wall
SOURCES = main.cpp foo.cpp bar.cpp
OBJECTS = $(SOURCES:.cpp=.o)

main: $(OBJECTS)
    $(CXX) $(CXXFLAGS) -o main $(OBJECTS)

%.o: %.cpp
    $(CXX) $(CXXFLAGS) -c $< -o $@
```

Here, we define the `SOURCES` variable to include all the C++ source files. The `OBJECTS` variable replaces the `.cpp` extension with `.o` to represent the object files. The target `main` depends on all the object files and is built by compiling each object file individually using the `%` wildcard rule.

## Cleaning Up with Phony Targets
Phony targets are targets that do not represent actual files but perform an action. They are commonly used for cleaning up generated files or executing specific tasks.

```makefile
.PHONY: clean

clean:
    rm -f $(OBJECTS) main
```

In this example, a phony target `clean` is defined to remove the object files and the compiled binary.

## Conclusion
Using a `Makefile` as a traditional C++ build system provides a flexible and customizable way to compile and manage C++ projects. It allows you to define targets, dependencies, and actions, making the build process more efficient and organized. With the knowledge gained from this blog post, you can start utilizing `make` and `Makefile` to improve your C++ development workflow.

\#c++ #buildsystem