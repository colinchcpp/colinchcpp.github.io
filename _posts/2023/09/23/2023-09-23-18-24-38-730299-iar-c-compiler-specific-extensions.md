---
layout: post
title: "IAR C++ Compiler-specific extensions"
description: " "
date: 2023-09-23
tags: [programming, embedded]
comments: true
share: true
---

The IAR C++ Compiler is a popular tool for developing embedded systems. It offers several compiler-specific extensions that can help optimize code and improve performance. In this blog post, we will explore some of the most important IAR C++ compiler extensions and how to use them effectively.

## 1. `__ramfunc`

When developing for embedded systems, it is often necessary to place critical functions in RAM for faster execution. The `__ramfunc` extension allows you to define a function that will be placed in RAM rather than flash memory. This can significantly improve the performance of time-critical code.

```c++
__ramfunc void criticalFunction() {
    // Code here
}
```

## 2. `__root`

The `__root` extension is used to ensure that a specific function or variable will always be included in the final executable, even if it is not directly referenced in the code. This can be useful for initialization functions or global variables that are required for the correct operation of the system.

```c++
__root void init() {
    // Initialization code
}
```

## Conclusion

The IAR C++ Compiler provides several useful extensions that can enhance code performance and functionality. The `__ramfunc` extension allows critical functions to be placed in RAM for faster execution, while `__root` ensures that specific functions or variables are always included in the final executable.

Using these compiler-specific extensions can help developers optimize their embedded systems and achieve better performance.

#programming #embedded