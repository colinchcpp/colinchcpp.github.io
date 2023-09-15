---
layout: post
title: "Controlling visibility and access of symbols in C++ Modules"
description: " "
date: 2023-09-15
tags: []
comments: true
share: true
---

C++ Modules provide a new way of organizing and managing code that enhances code reuse and improves build times. One of the important aspects of code organization is controlling the visibility and access of symbols within a module. In this blog post, we will explore how to achieve this in C++ Modules.

## Controlling Symbol Visibility

By default, in C++ Modules, all symbols declared in the module interface are visible outside of the module. However, there are scenarios where you may want to control the visibility of certain symbols. C++ Modules provide two ways to achieve this: hiding symbols and explicitly exporting symbols.

### Hiding Symbols

To hide symbols within a C++ Module, you can use the `hidden` keyword. When you declare a symbol with the `hidden` keyword, it is not visible outside of the module. This can be useful when you want to encapsulate implementation details and prevent other modules from accessing certain symbols.

```cpp
module math;

export module math;

int add(int a, int b);
int multiply(int a, int b);

hidden int subtract(int a, int b); // hide the subtract function
```

In the above example, the `subtract` function is declared as `hidden`, making it invisible to other modules that import the `math` module.

### Explicitly Exporting Symbols

On the other hand, you can explicitly export symbols in your C++ Modules using the `export` keyword. When you export a symbol, it becomes visible outside of the module. This can be useful when you want to expose specific symbols to other modules.

```cpp
module math;

export module math;

export int add(int a, int b); // explicitly export the add function
export int multiply(int a, int b);
```

In the above example, the `add` function is explicitly exported, making it visible to other modules that import the `math` module.

## Controlling Symbol Access

In addition to controlling symbol visibility, C++ Modules also allow you to control symbol access within a module. This can be achieved by using the `import` statement inside a module implementation.

```cpp
module math;

export module math;

int add(int a, int b);
int multiply(int a, int b); 

export {
    import hidden int subtract(int a, int b); // import the subtract function for internal use
}
```

In the above example, the `subtract` function is imported with the `hidden` visibility specifier. This allows the `subtract` function to be used internally within the module, but it is not visible outside of the module.

## Conclusion

Controlling symbol visibility and access within C++ Modules allows for better code organization and encapsulation. By using the `hidden` and `export` keywords, you can selectively hide or expose symbols to other modules. Additionally, the `import` statement enables you to control symbol access within a module. Overall, these features enhance code reuse and improve the manageability of C++ codebases.

#C++ #C++Modules