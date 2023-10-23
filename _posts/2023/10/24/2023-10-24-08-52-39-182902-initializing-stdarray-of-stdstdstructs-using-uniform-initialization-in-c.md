---
layout: post
title: "Initializing std::array of std::std::structs using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, the `std::array` container provides a fixed-size array-like data structure with compile-time size checking. With the introduction of uniform initialization in C++11, initializing `std::array` of `structs` becomes easier and more concise. In this blog post, we will explore how to initialize a `std::array` of `structs` using uniform initialization in C++.

Creating a Struct

Let's start by defining a simple `struct` that we want to store in our `std::array`:

```cpp
struct Person {
    std::string name;
    int age;
};
```

Here, we have a `Person` struct with two members: `name` of type `std::string` and `age` of type `int`.

Initializing std::array Using Uniform Initialization

To create a `std::array` of `Person` structs and initialize it using uniform initialization, we can follow these steps:

1. Include the necessary headers:

```cpp
#include <array>
#include <string>
```

2. Declare and initialize the `std::array` as follows:

```cpp
std::array<Person, 3> personArray = {
    {"Alice", 25},
    {"Bob", 30},
    {"Charlie", 35}
};
```

In the above code, we declare and initialize a `std::array` named `personArray` with a size of 3. We use uniform initialization to provide the initial values for each `Person` struct element.

Accessing the Elements

Once we have initialized the `std::array`, we can access its elements using the usual array indexing syntax. For example, to access the name and age of the first person in the array:

```cpp
std::cout << "Name: " << personArray[0].name << ", Age: " << personArray[0].age << std::endl;
```

This will output:

```
Name: Alice, Age: 25
```

Conclusion

Initializing a `std::array` of `structs` using uniform initialization in C++ is a convenient way to initialize multiple elements at once. By utilizing the power of uniform initialization, we can easily create and initialize complex data structures like arrays of `structs` in a concise and readable manner.

References:
- [C++ std::array documentation](https://en.cppreference.com/w/cpp/container/array)
- [C++11 Uniform Initialization](https://en.cppreference.com/w/cpp/language/initializer_list)