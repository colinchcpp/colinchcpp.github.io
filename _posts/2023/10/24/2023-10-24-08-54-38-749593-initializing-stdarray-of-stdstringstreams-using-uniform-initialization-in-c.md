---
layout: post
title: "Initializing std::array of std::stringstreams using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

First, include the necessary header files:
```cpp
#include <array>
#include <sstream>
```

Next, declare the std::array with the desired number of std::stringstreams:
```cpp
std::array<std::stringstream, 3> myArray;
```

Now, you can use uniform initialization to initialize each std::stringstream within the std::array. Here's an example of how you can do this:
```cpp
myArray = {std::stringstream(), std::stringstream(), std::stringstream()};
```

This will create an std::array containing three std::stringstream objects. Each std::stringstream is initialized with the default constructor.

You can also directly insert values into the std::stringstreams during initialization:
```cpp
myArray = {std::stringstream("Hello"), std::stringstream("World"), std::stringstream("C++")};
```

In this case, each std::stringstream is initialized with a string argument.

Remember to include the necessary headers, and make sure the array size matches the number of elements you want to initialize.

Using uniform initialization in C++ allows for concise and clean code when initializing an std::array of std::stringstreams.

References:
- [std::array - C++ Reference](https://en.cppreference.com/w/cpp/container/array)
- [std::stringstream - C++ Reference](https://en.cppreference.com/w/cpp/io/basic_stringstream)

#cpp #C++