---
layout: post
title: "Initializing std::array of structs using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: [uniform, UniformInitialization]
comments: true
share: true
---

Let's say we have a struct defined as follows:

```cpp
struct Person {
    std::string name;
    int age;
};
```

We can initialize a `std::array` of `Person` structs using uniform initialization as follows:

```cpp
{% raw %}
std::array<Person, 3> people = {{
    {"Alice", 25},
    {"Bob", 30},
    {"Charlie", 35}
}};
{% endraw %}
```
{% raw %}
In the above code example, we define a `std::array` called `people` that can store three `Person` objects. Each object is initialized using a brace-enclosed list. The double braces `{{ }}` are used to indicate initialization of the array, while the inner braces `{ }` are used for initializing each individual `Person` struct.
{% endraw %}
You can add or modify the number of elements in the `std::array` as needed, and provide the corresponding initializations for each struct.

Uniform initialization not only works with `std::array`, but it is also supported for other container types and custom classes. This syntax provides a consistent and intuitive way to initialize objects in C++.

By using uniform initialization, you can make your code more concise and readable, especially when initializing complex data structures. It can help to improve code maintainability and reduce the chance of initialization errors.

For more information, you can refer to the following references:

- [cppreference: Uniform initialization](https://en.cppreference.com/w/cpp/language/initialization)
- [C++17: The Complete Guide - Uniform Initialization](https://www.modernescpp.com/index.php/c-core-guidelines-constructors-and-initialization#uniform-initialization) 

```markdown
# Initializing std::array of structs using uniform initialization in C++

In C++, you can initialize a `std::array` of structs using uniform initialization. Uniform initialization provides a concise and readable way to initialize objects.

Let's say we have a struct defined as follows:

```cpp
struct Person {
    std::string name;
    int age;
};
```

We can initialize a `std::array` of `Person` structs using uniform initialization as follows:

```cpp
{% raw %}
std::array<Person, 3> people = {{
    {"Alice", 25},
    {"Bob", 30},
    {"Charlie", 35}
}};
{% endraw %}
```

In the above code example, we define a `std::array` called `people` that can store three `Person` objects. Each object is initialized using a brace-enclosed list. The double braces `{{ }}` are used to indicate initialization of the array, while the inner braces `{ }` are used for initializing each individual `Person` struct.

You can add or modify the number of elements in the `std::array` as needed, and provide the corresponding initializations for each struct.

Uniform initialization not only works with `std::array`, but it is also supported for other container types and custom classes. This syntax provides a consistent and intuitive way to initialize objects in C++.

By using uniform initialization, you can make your code more concise and readable, especially when initializing complex data structures. It can help to improve code maintainability and reduce the chance of initialization errors.

For more information, you can refer to the following references:

- [cppreference: Uniform initialization](https://en.cppreference.com/w/cpp/language/initialization)
- [C++17: The Complete Guide - Uniform Initialization](https://www.modernescpp.com/index.php/c-core-guidelines-constructors-and-initialization#uniform-initialization) 

## Conclusion
Uniform initialization provides a convenient way to initialize `std::array` of structs and other objects in C++, leading to more readable and maintainable code.

## #C++ #UniformInitialization