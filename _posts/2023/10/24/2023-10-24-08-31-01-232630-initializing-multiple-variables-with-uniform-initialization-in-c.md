---
layout: post
title: "Initializing multiple variables with uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, you can use uniform initialization to initialize multiple variables in a single line of code. This approach helps improve readability and reduces the chances of forgetting to initialize a variable. 

To initialize multiple variables with uniform initialization, you can use curly braces {} and separate each variable assignment with a comma. Here's an example:

```cpp
int x{ 10 }, y{ 20 }, z{ 30 };
```

In the above code snippet, three variables `x`, `y`, and `z` are initialized with values 10, 20, and 30 respectively. 

Uniform initialization works not only for built-in types but also for user-defined types such as classes and structs. Here's an example:

```cpp
class MyClass {
public:
    int value;
    std::string text;
};

MyClass obj{ 42, "Hello World" };
```

In this example, the `MyClass` object `obj` is initialized with `value` set to 42 and `text` set to "Hello World".

Uniform initialization is not only limited to initializing variables but can also be used when passing arguments to functions or constructors. 

```cpp
void myFunction(int a, int b, int c) {
    // function logic
}

myFunction({ 1, 2, 3 }); // Using uniform initialization to pass arguments
```

In this case, the `myFunction` is called with three integers passed using uniform initialization.

Uniform initialization provides a concise and consistent syntax to initialize multiple variables or pass arguments. It is recommended to use uniform initialization whenever possible, as it promotes cleaner and more readable code.

References:
- [C++11 Uniform Initialization](https://en.cppreference.com/w/cpp/language/list_initialization)
- [Effective Modern C++ by Scott Meyers](https://www.amazon.com/Effective-Modern-Specific-Ways-Improve/dp/1491903996)

#C++ #Initialization