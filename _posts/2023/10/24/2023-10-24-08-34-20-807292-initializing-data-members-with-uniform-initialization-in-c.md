---
layout: post
title: "Initializing data members with uniform initialization in C++"
description: " "
date: 2023-10-24
tags: [Initialization]
comments: true
share: true
---

One of the main features introduced in C++11 is the uniform initialization syntax. With uniform initialization, you can initialize data members of a class or struct using a consistent and concise syntax. This syntax is not only simpler to read and write but also provides better type checking.

## Traditional Initialization in C++

Before C++11, initializing data members could be done using different syntaxes depending on the context. For example:

```cpp
class MyClass {
public:
    int num;
    std::string name;
    float value;
};

int main() {
    MyClass obj;
    obj.num = 10;
    obj.name = "John";
    obj.value = 3.14f;

    return 0;
}
```

In the above example, we first declare an instance of the `MyClass` class called `obj`. Then, we assign values to its data members `num`, `name`, and `value` using the assignment operator.

## Uniform Initialization Syntax in C++11

With C++11 and later versions, you can use the uniform initialization syntax to initialize data members directly when declaring an object. The syntax is as follows:

```cpp
class MyClass {
public:
    int num;
    std::string name;
    float value;
};

int main() {
    MyClass obj{10, "John", 3.14f};

    return 0;
}
```

In the updated example above, we declare an instance of `MyClass` called `obj` and initialize its data members `num`, `name`, and `value` directly within the braces `{}`. This syntax provides a more concise and consistent way of initializing data members.

## Benefits of Uniform Initialization

1. **Consistency:** The uniform initialization syntax allows you to initialize data members in a consistent manner, regardless of the context. Whether you're initializing within a class or struct definition, or during object declaration, the syntax remains the same.

2. **Improved Type Safety:** The uniform initialization syntax performs better type checking by disallowing narrowing conversions. This means that if a narrowing conversion occurs during initialization (e.g., from floating-point to integer), a compilation error will be issued. This helps to catch potential bugs early on.

## Conclusion

Uniform initialization syntax introduced in C++11 provides a cleaner and more consistent way to initialize data members of classes and structs. It simplifies the initialization process, enhances code readability, and offers better type safety. By adopting this syntax, you can write more expressive and robust code in your C++ programs.

**References**

1. [C++ initializer list](https://en.cppreference.com/w/cpp/language/initializer_list)
2. [C++ tutorial: Uniform initialization](https://www.learncpp.com/cpp-tutorial/uniform-initialization/) #C++ #Initialization