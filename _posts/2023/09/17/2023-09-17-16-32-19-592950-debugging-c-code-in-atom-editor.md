---
layout: post
title: "Debugging C++ code in Atom editor"
description: " "
date: 2023-09-17
tags: [AtomEditor]
comments: true
share: true
---

Atom editor is a popular and highly customizable text editor that supports numerous programming languages, including C++. While Atom does not come with built-in debugging capabilities, you can extend its functionality by installing plugins that provide debugging features.

In this article, we will explore how to set up and use the **`atom-ide-debugger-cpp`** plugin to debug C++ code in Atom.

## Prerequisites
Before we begin, ensure that you have the following prerequisites in place:

1. **Atom Editor**: If you haven't already, download and install the Atom editor from the official website (https://atom.io).

2. **GCC**: Make sure you have GCC (GNU Compiler Collection) installed on your system. This is required to compile and run C++ code.

## Installing the atom-ide-debugger-cpp plugin
To enable C++ debugging in Atom, follow these steps:

1. Launch Atom and go to **File > Settings > Install**.

2. In the search box, type **`atom-ide-debugger-cpp`** and click on the **Install** button next to the plugin.

3. Once the installation is complete, you will have to configure the plugin.

## Configuring the atom-ide-debugger-cpp plugin
To configure the **atom-ide-debugger-cpp** plugin, follow these steps:

1. Open your project in Atom.

2. Create a `.vscode` folder in the root directory of your project if it doesn't exist already.

3. Inside the `.vscode` folder, create a `launch.json` file.

4. Add the following content to `launch.json`:

   ```json
   {
     "version": "0.2.0",
     "configurations": [
       {
         "name": "C++ Debug",
         "type": "cppdbg",
         "request": "launch",
         "program": "${workspaceFolder}/<your_executable_name>",
         "args": [],
         "stopAtEntry": false,
         "cwd": "${workspaceFolder}",
         "environment": [],
         "externalConsole": true,
         "MIMode": "gdb"
       }
     ]
   }
   ```

   Make sure to replace `<your_executable_name>` with the name of your C++ executable file.

5. Save the `launch.json` file.

## Debugging C++ code in Atom
To start debugging your C++ code in Atom, follow these steps:

1. Ensure that you have a breakpoint set in your code by placing the cursor on the desired line and pressing **`F9`**.

2. Open the file you want to debug.

3. Press **`F5`** or go to **Packages > atom-ide-debugger-cpp > Debug: Start Debugging** to start the debugging session.

4. The debugger will pause your program at the breakpoint, allowing you to inspect variables, step through code, and track down errors.

## Conclusion
By installing and configuring the **atom-ide-debugger-cpp** plugin, you can enhance Atom's functionality and debug your C++ code effectively. With breakpoints, variable inspection, and step-through capabilities, debugging C++ in Atom becomes more efficient.

Give it a try and streamline your C++ development workflow in the Atom editor!

**#AtomEditor #C++Debugging**