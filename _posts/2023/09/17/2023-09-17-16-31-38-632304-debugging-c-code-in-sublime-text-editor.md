---
layout: post
title: "Debugging C++ code in Sublime Text editor"
description: " "
date: 2023-09-17
tags: [programming, debugging]
comments: true
share: true
---

## Prerequisites

Before we dive into the debugging process, make sure you have the following:

- Sublime Text editor installed on your machine.
- C++ compiler (such as GCC or Clang) set up and working.

## Setting up Sublime Text for C++ debugging

To enable C++ debugging in Sublime Text, you'll need to install a third-party package called **SublimeGDB**. Follow these steps to set it up:

1. Open Sublime Text.
2. Press `Ctrl + Shift + P` (or `Cmd + Shift + P` on macOS) to open the Command Palette.
3. Type "Package Control: Install Package" and press Enter.
4. Search for "SublimeGDB" and select it to install.

## Creating a debug configuration file

Once you have SublimeGDB installed, you need to create a debug configuration file for your C++ project. This file specifies the necessary settings for debugging. 

Create a new file and save it with a `.gdb` extension, for example, `debug.gdb`. Inside this file, add the following configuration:

```gdb
file <path_to_executable>
```

Replace `<path_to_executable>` with the path to your compiled C++ executable.

## Starting the debugging session

To start a debugging session in Sublime Text, follow these steps:

1. Open the C++ file you want to debug.
2. Set breakpoints by clicking on the gutter at the left side of the code editor or by pressing `F9`.
3. Press `Ctrl + Shift + P` (or `Cmd + Shift + P` on macOS) to open the Command Palette.
4. Type "GDB: Start debugging" and press Enter.

SublimeGDB will start the debugging session, and execution will pause at the first breakpoint encountered.

## Debugging with Sublime Text

Sublime Text provides several debugging commands to help you navigate through your code during a debugging session. Here are a few essential commands:

- `F5`: Continue execution until the next breakpoint or until the program finishes.
- `F10`: Step over the current line.
- `F11`: Step into a function call.
- `Shift + F11`: Step out of the current function.

You can also view variables, inspect the call stack, and evaluate expressions during the debugging process.

## Conclusion

Debugging C++ code in Sublime Text can streamline the software development process and help identify and fix issues quickly. By following the steps outlined in this blog post, you can set up Sublime Text for C++ debugging and utilize the debugging commands to efficiently debug your code.

#programming #debugging #C++