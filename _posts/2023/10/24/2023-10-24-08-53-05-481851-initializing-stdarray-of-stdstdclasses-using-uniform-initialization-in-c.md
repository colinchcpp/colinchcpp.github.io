---
layout: post
title: "Initializing std::array of std::std::classes using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Uniform initialization allows you to initialize an object using braces `{}`. When it comes to `std::array`, you can use uniform initialization to initialize the elements of the array directly at the time of declaration.

Here is an example of how to initialize a `std::array` of `std::string` using uniform initialization:

```cpp
#include <array>
#include <string>

int main() {
    std::array<std::string, 3> myArray = { "Hello", "World", "!" };
    
    // Accessing elements of the array
    std::cout << myArray[0] << " " << myArray[1] << myArray[2] << std::endl;
    
    return 0;
}
```

In this code snippet, we declare a `std::array` called `myArray` of type `std::string` with a size of 3. We use the uniform initialization syntax `{}` to assign values to the elements of the array.

After initialization, we can access the elements of the array using the subscript operator `[]`. In this case, we print the elements of the array, which yields the output: "Hello World!".

The use of uniform initialization with `std::array` provides a clean and concise way to initialize the elements of the array at declaration. It avoids the need for explicit element-wise initialization, especially when dealing with larger arrays.

Overall, uniform initialization simplifies the process of initializing `std::array` objects and improves code readability. It is a useful feature to leverage when working with arrays in C++.