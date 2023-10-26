---
layout: post
title: "Initializing std::array of classes using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

To initialize a std::array of classes using uniform initialization, follow these steps:

1. Include the <array> header file at the beginning of your code:
```cpp
#include <array>
```

2. Define your class with a constructor:
```cpp
class MyClass {
public:
    int value;
    
    MyClass(int val) : value(val) {}
};
```

3. Use the std::array class and initialize it with the desired values using uniform initialization syntax:
```cpp
std::array<MyClass, 3> myArray{ {1}, {2}, {3} };
```
In this example, we are initializing a std::array called `myArray` of size 3. Each element of the array is of type MyClass. We are using uniform initialization syntax to initialize the objects of MyClass with different values.
{% raw %}
Note the use of double braces `{{ }}` when initializing the elements of the std::array. This is required because the elements of the array are themselves objects of the class MyClass.
{% endraw %}
Now you can access the elements of the std::array and their members using the usual array indexing syntax:
```cpp
int secondValue = myArray[1].value;
```

Uniform initialization provides a concise and consistent way to initialize arrays of classes and other objects in C++. It helps avoid errors and makes the code more readable.

To learn more about std::array and uniform initialization in C++, you can refer to the following references:
- [std::array - C++ Reference](https://en.cppreference.com/w/cpp/container/array)
- [Uniform initialization - C++ Reference](https://en.cppreference.com/w/cpp/language/initialization)

#cplusplus #uniforminitialization