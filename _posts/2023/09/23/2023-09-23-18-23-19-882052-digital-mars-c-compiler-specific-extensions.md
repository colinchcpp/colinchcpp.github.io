---
layout: post
title: "Digital Mars C++ Compiler-specific extensions"
description: " "
date: 2023-09-23
tags: [extensions]
comments: true
share: true
---

The Digital Mars C++ Compiler, also known as DMC++ or simply "Digital Mars," is a C++ compiler that provides a variety of extensions and features beyond the standard C++ language. These extensions are specific to the Digital Mars compiler and may not be available or behave differently in other compilers.

## \#1. Fastcall Calling Convention

One of the notable extensions provided by Digital Mars is the `fastcall` calling convention. This convention allows for faster function calls by passing arguments through registers rather than the stack. To use this convention, simply add the `fastcall` keyword before the function declaration:

```cpp
fastcall int myFunction(int a, int b) { ... }
```

Using the `fastcall` calling convention can lead to improved performance in cases where many function calls are made.

## \#2. Near and Far Pointers

Digital Mars also supports the use of `near` and `far` keyword qualifiers for pointers, providing control over the assumed memory model. These qualifiers were commonly used in older versions of C/C++, particularly in MS-DOS programming.

For example, to declare a near pointer, use the `near` keyword:

```cpp
int near* pNearData;
```

To declare a far pointer, use the `far` keyword:

```cpp
int far* pFarData;
```

These qualifiers dictate how pointers behave in segmented memory models, allowing you to write code that targets specific memory addressing schemes.

Please note that these pointer qualifiers have limited relevance in modern systems and are primarily provided for compatibility with legacy code.

## Conclusion

The Digital Mars C++ Compiler offers various extensions and features beyond the standard C++ language. These extensions, such as the `fastcall` calling convention and the `near` and `far` pointer qualifiers, can be useful in specific scenarios and for maintaining compatibility with older codebases.

While these Digital Mars-specific extensions can enhance the power and flexibility of the compiler, it's important to remember that they may not be supported or behave the same way in other C++ compilers. Therefore, it is essential to consider the portability of your code when utilizing these extensions.

\#dmc++ #c++compiler #extensions