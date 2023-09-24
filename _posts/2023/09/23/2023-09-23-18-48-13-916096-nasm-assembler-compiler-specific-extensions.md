---
layout: post
title: "NASM Assembler Compiler-specific extensions"
description: " "
date: 2023-09-23
tags: [assembly, nasm]
comments: true
share: true
---

NASM (Netwide Assembler) is a popular assembler for the x86 architecture. It provides a range of features and directives that make assembly programming more powerful and efficient. In addition to the standard x86 instruction set, NASM also supports compiler-specific extensions, which provide further functionality for specific compilers.

In this blog post, we will explore some of the compiler-specific extensions available in NASM and how they can be utilized to enhance your assembly programming experience. Let's dive in!

## 1. Microsoft Macro Assembler (MASM) compatible syntax

NASM provides support for the Microsoft Macro Assembler (MASM) compatible syntax. This syntax allows you to write assembly code that is compatible with MASM, a widely used assembler for the x86 architecture. To enable MASM compatible syntax in NASM, use the directive `--prefix _` at the beginning of your assembly program.

```nasm
--prefix _
```

With MASM compatible syntax, you can directly use MASM-style directives and instructions in your NASM code, making it easier to port existing MASM code to NASM or work with MASM-compatible libraries.

## 2. GNU Assembler (GAS) compatible syntax

NASM also provides support for the GNU Assembler (GAS) compatible syntax. GAS is the default assembler used by the GNU Compiler Collection (GCC). To enable GAS compatible syntax in NASM, use the directive `%pragma gas`.

```nasm
%pragma gas
```

Using GAS compatible syntax allows you to write assembly code that is compatible with GAS, making it easier to integrate NASM code with GCC-based projects or reuse existing GAS code in NASM.

## Conclusion

NASM's compiler-specific extensions provide a seamless experience for assembly programmers who are familiar with MASM or GAS syntax. Enabling MASM compatible syntax with the `--prefix _` directive allows the use of MASM-style directives and instructions. Similarly, enabling GAS compatible syntax with the `%pragma gas` directive facilitates integration with GCC projects.

By leveraging these extensions, you can write assembly code that is compatible with different compilers, reuse existing code, and seamlessly integrate assembly modules into larger projects. This flexibility makes NASM a powerful choice for assembly programming enthusiasts.

#assembly #nasm #masm #gas