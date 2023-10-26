---
layout: post
title: "Initializing std::array of std::arrays using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

1. Include the necessary headers:
```cpp
#include <array>
```

2. Declare the outer std::array container with the desired size and the inner std::array container with the appropriate size of each array element:
```cpp
std::array<std::array<int, 3>, 2> myArray;
```
In this example, we declared an outer std::array with a size of 2, and each element is a std::array with a size of 3.

3. Initialize the std::array of std::arrays using uniform initialization syntax:
```cpp
{% raw %}
std::array<std::array<int, 3>, 2> myArray = {{
    {1, 2, 3},
    {4, 5, 6}
}};
{% endraw %}
```
In this example, we initialize the outer std::array using two inner std::array elements, each containing three integers.

Here's a complete example:

```cpp
{% raw %}
#include <iostream>
#include <array>

int main() {
    std::array<std::array<int, 3>, 2> myArray = {{
        {1, 2, 3},
        {4, 5, 6}
    }};
    
    // Access and print the values
    for (const auto& innerArray : myArray) {
        for (const auto& element : innerArray) {
            std::cout << element << " ";
        }
        std::cout << "\n";
    }
    
    return 0;
}
{% endraw %}
```

This code initializes a 2-dimensional std::array with 2 rows and 3 columns using uniform initialization. The values are then printed using nested loops.

By using uniform initialization, we can easily initialize complex data structures like std::array of std::arrays in a concise and readable manner.

Remember to include the `<array>` header for using std::array, and compile your code with a C++11 or newer standard.

For more information, you can refer to the following references:

- [std::array - C++ Reference](https://en.cppreference.com/w/cpp/container/array)
- [C++ Standard Library](https://en.cppreference.com/w/cpp/header/array)

#cpp #cplusplus