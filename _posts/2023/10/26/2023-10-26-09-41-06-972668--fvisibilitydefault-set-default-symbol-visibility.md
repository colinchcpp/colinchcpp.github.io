---
layout: post
title: "-fvisibility=default (set default symbol visibility)"
description: " "
date: 2023-10-26
tags: []
comments: true
share: true
---

In certain programming languages, such as C++, you have the ability to control the visibility of symbols in your code. The visibility of a symbol determines whether it can be accessed from outside of the current module or library. By default, symbols are typically set to be globally visible, meaning they can be accessed from anywhere.

However, in some cases, you may want to restrict the visibility of symbols to improve encapsulation and prevent unintended usage. This is where the `-fvisibility=default` option comes into play.

In this blog post, we will explore the purpose and usage of the `-fvisibility=default` option and understand how it affects the visibility of symbols in your code.

### Understanding Symbol Visibility

Symbol visibility refers to the scope at which a symbol (such as a function or variable) can be accessed. In a programming language like C++, symbols declared without any visibility attributes are by default globally visible, meaning they can be accessed from any module or library that links against them.

The concept of symbol visibility is particularly important when creating libraries or shared objects. You may want to control which symbols are exposed to the outside world and which ones are kept private to the internal implementation.

### Introducing the `-fvisibility=default` Option

The `-fvisibility=default` option is a compiler setting that sets the default symbol visibility for all symbols in your codebase. When you use this option, any symbol that is not explicitly annotated with a visibility attribute will inherit the default visibility level.

By setting `-fvisibility=default`, you are essentially asking the compiler to use the default visibility rules defined by the compiler or the operating system.

### Controlling Symbol Visibility

To control the visibility of a symbol, you can use visibility attributes provided by the compiler. These attributes allow you to mark symbols as either visible or hidden.

When a symbol is marked as visible, it can be accessed from outside the module or library. On the other hand, when a symbol is marked as hidden, it can only be accessed from within the module or library.

Here's an example of how you can use visibility attributes:

```cpp
// Declare a globally visible function
__attribute__((visibility("default"))) void myPublicFunction() {
  // Function implementation
}

// Declare a hidden function
__attribute__((visibility("hidden"))) void myPrivateFunction() {
  // Function implementation
}
```

By explicitly setting the visibility attribute for each symbol, you can have fine-grained control over which symbols are visible to external code.

### Conclusion

The `-fvisibility=default` option in compiler settings allows you to set the default symbol visibility for your code. By using this option, you can control which symbols are visible outside of your module or library.

Remember that symbol visibility is an important concept, especially when working with libraries or shared objects. By using visibility attributes, you can mark symbols as either visible or hidden, providing better encapsulation and control over your codebase.

Be sure to consult the documentation of your specific compiler for more details on how to use `-fvisibility=default` and visibility attributes for symbol control.

## References
- [GCC Visibility](https://gcc.gnu.org/wiki/Visibility)