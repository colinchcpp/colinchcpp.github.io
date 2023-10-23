---
layout: post
title: "Uniform initialization for non-static data members in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, non-static data members of a class can be initialized using the uniform initialization syntax. This syntax allows you to initialize the data members of an object in a more concise and readable way. This feature was introduced in C++11.

To initialize a non-static data member using uniform initialization, you can use the initializer list syntax in the constructor of the class. Let's consider an example of a class `Person` with non-static data members `name` and `age`:

```cpp
class Person {
public:
    std::string name;
    int age;

    Person(const std::string& n, int a) : name{n}, age{a} {}
};
```

In the above example, we are using the uniform initialization syntax to initialize the `name` and `age` members of the `Person` class. The `name` member is initialized using the expression `name{n}`, where `n` is the constructor parameter `n`. Similarly, the `age` member is initialized using the expression `age{a}`.

By using uniform initialization, you can initialize non-static data members with the following benefits:

1. Readability: The syntax is more concise and clear, making the initialization code easier to understand.
2. Consistency: Uniform initialization syntax can be used consistently for initializing both non-static data members and constructor parameters.
3. Initialization of complex objects: You can use uniform initialization to initialize non-static data members of complex objects like containers, arrays, and other user-defined types.

Here's an example of how to create an instance of the `Person` class using uniform initialization:

```cpp
Person person{"John Doe", 30};
```

In the above example, we are creating a `Person` object named `person` and initializing the `name` member with the string "John Doe" and the `age` member with the value 30.

In conclusion, uniform initialization for non-static data members in C++ allows for more concise and readable initialization syntax, ensuring consistency and improving code readability. It is a useful feature, especially when dealing with complex object initialization.

**References:**
- [C++ documentation on uniform initialization](https://en.cppreference.com/w/cpp/language/initializer_list)