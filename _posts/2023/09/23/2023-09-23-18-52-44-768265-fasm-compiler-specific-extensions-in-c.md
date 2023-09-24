---
layout: post
title: "FASM Compiler-specific extensions in C++"
description: " "
date: 2023-09-23
tags: [include, assembly]
comments: true
share: true
---

FASM is a popular assembly language compiler that provides extensions to the assembly syntax for enhanced functionality and flexibility. In this blog post, we will explore how to leverage these extensions in C++ code for optimized assembly-level programming with the FASM compiler.

## Inline Assembly 

One of the main features of FASM is its support for inline assembly code within C++ programs. This allows you to embed assembly instructions directly within your C++ source code, providing fine-grained control over the generated machine code.

To use inline assembly with FASM, you need to wrap your assembly instructions within the `__asm__` keyword. Here's an example of how you can use inline assembly in C++:

```c++
#include <iostream>

int main() {
    int a = 10, b = 20, result;
    
    __asm__ (
        "add %1, %2\n\t"
        "mov %0, %1"
        : "=r" (result) 
        : "r"(a), "r"(b)
    );
    
    std::cout << "Result: " << result << std::endl;
    
    return 0;
}
```

In the above code, the `add` and `mov` instructions are written directly in assembly syntax within the `__asm__` block. The input (`a` and `b`) and output (`result`) operands are specified using the `%0`, `%1`, and `%2` placeholders. The constraints `"=r"` and `"r"` specify that the operands should be resolved into registers.

## FASM Compiler Directives

FASM also provides several compiler-specific directives that enable advanced assembly-level programming techniques. These directives allow you to control various aspects of the assembly code generation process, including memory layout, optimizations, and code organization.

Here are some commonly used FASM compiler directives:

### `%define`

The `%define` directive allows you to define symbolic constants that can be used in your assembly code. This can be particularly useful for improving code readability and maintainability. For example:

```assembly
%define MAX_LOOP_COUNT 10

    mov ecx, MAX_LOOP_COUNT
    ...
```

### `%macro`

The `%macro` directive provides a way to define reusable assembly code macros. Macros can be used to encapsulate frequently used code snippets and simplify code duplication. For instance:

```assembly
%macro ADD_TWO_NUMBERS 3

    mov eax, %1
    add eax, %2
    mov %3, eax

%endmacro

ADD_TWO_NUMBERS 10, 20, result
```

### `%include`

The `%include` directive enables you to include external assembly source files into your project. This can be useful for modularizing your codebase and reusing common utility functions. For example:

```assembly
%include "utils.asm"

main:
    ...
```

## Conclusion

By leveraging the FASM compiler-specific extensions in C++, you can take advantage of inline assembly code and various directives to write highly optimized and efficient code at the assembly level. Whether you need fine-grained control over performance or low-level system access, FASM provides the flexibility to achieve your goals.

To dive deeper into FASM's capabilities, refer to the official FASM documentation and explore the extensive range of features and syntax available.

#assembly #FASM