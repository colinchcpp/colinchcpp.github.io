---
layout: post
title: "-fpic (like -fPIC but constraints the code interworking with non-PIC code)"
description: " "
date: 2023-10-26
tags: []
comments: true
share: true
---

In C and C++ programming languages, the `-fpic` flag is used during compilation to generate position-independent code (PIC). This flag is often used to create shared libraries (also known as dynamically linked libraries) that can be loaded and executed at different memory locations.

The `-fpic` flag is a variant of the `-fPIC` flag, and its primary difference lies in the code interworking constraints. While `-fPIC` allows the generated code to interwork with both PIC and non-PIC code, `-fpic` restricts the interworking only with non-PIC code. This means that the resulting code will not be able to call or be called by PIC code.

When compiling code with the `-fpic` flag, the compiler will ensure that all memory references are relative rather than absolute. This allows the code to be relocated and executed correctly regardless of where it is loaded into memory.

Here is an example of how the `-fpic` flag can be used in compilation:

```cpp
gcc -fpic -c mylibrary.c -o mylibrary.o
gcc -shared -o libmylibrary.so mylibrary.o
```

In this example, we compile the `mylibrary.c` source file with the `-fpic` flag to generate the `mylibrary.o` object file. We then use the `-shared` flag to link the object file into a shared library named `libmylibrary.so`.

It is important to note that the use of the `-fpic` flag may result in slightly larger code compared to non-PIC code, as it requires additional instructions to perform relative memory addressing. However, the advantage of generating position-independent code outweighs the increase in code size when creating shared libraries.

By utilizing the `-fpic` flag, developers can create portable shared libraries that can be loaded and executed at different memory locations without compatibility issues.

*References:*
- GCC Documentation: [Options for Code Generation Conventions](https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html)
- IBM Developer: [Position-Independent Code (PIC) in Shared Libraries](https://developer.ibm.com/articles/pic-and-shared-libraries/)