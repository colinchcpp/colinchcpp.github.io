---
layout: post
title: "Initializing std::vector using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

C++11 introduced uniform initialization syntax that allows initializing containers like `std::vector` in a concise and easy-to-read manner.

Instead of using the traditional constructor syntax, you can use the brace initialization syntax to initialize a `std::vector` using uniform initialization. This syntax uses a pair of braces `{}` to delimit the initialization list.

Here's an example of how you can initialize a `std::vector` using uniform initialization:

```cpp
#include <iostream>
#include <vector>

int main() {
    // Initializing vector of integers using uniform initialization
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // Printing the vector elements
    for (const auto& number : numbers) {
        std::cout << number << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the code above, we first include the required headers (`<iostream>` and `<vector>`). Then, we declare a `std::vector` of integers named `numbers` and initialize it using uniform initialization with the values `{1, 2, 3, 4, 5}`.

Finally, we iterate over the elements of the vector using a range-based for loop and print each element to the console.

When you run the above code, it will output: `1 2 3 4 5`, indicating that the vector has been successfully initialized using uniform initialization.

Uniform initialization provides a more modern and concise way to initialize containers like `std::vector` in C++. It simplifies the syntax and makes the code more readable.

*References:*
- [cplusplus.com - std::vector](http://www.cplusplus.com/reference/vector/vector/)
- [cppreference.com - Uniform initialization syntax](https://en.cppreference.com/w/cpp/language/list_initialization)