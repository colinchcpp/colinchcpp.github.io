---
layout: post
title: "Improved lambda capture"
description: " "
date: 2023-09-29
tags: [programming, include]
comments: true
share: true
---

Lambda functions are a powerful feature in C++, allowing you to define anonymous functions on-the-fly. One of the key features of lambda functions is the ability to capture variables from their surrounding context. In C++11 and C++14, capturing variables in lambda functions was limited to only capturing by value or capturing by reference. However, in C++14, an improvement was introduced - the ability to capture variables by move semantics.

Capturing by value makes a copy of the variable, while capturing by reference refers to the original variable. The new improvement in C++14 allows you to capture by move semantics, which is especially useful for large, non-copyable objects.

To capture a variable by move semantics in a lambda function, you can use the new capture specifier `&&`. This tells the lambda function to capture the variable by moving it instead of making a copy or capturing by reference. Here's an example to demonstrate how this works:

```cpp
#include <iostream>
#include <vector>

int main() {
  std::vector<int> numbers = {1, 2, 3, 4, 5};

  auto lambda = [numbers = std::move(numbers)]() {
    // Use the captured variable by move
    for (int number : numbers) {
      std::cout << number << " ";
    }
  };

  lambda(); // Output: 1 2 3 4 5

  // Since numbers was moved, it is now in a valid but unspecified state
  return 0;
}
```

In the example above, we have a vector of numbers that we want to capture by move in the lambda function. We use the new capture specifier `numbers = std::move(numbers)` to move the vector into the lambda function.

Using variables with move semantics in lambda functions can lead to more efficient code. Instead of making unnecessary copies, the original object is moved into the lambda. It is important to note that after the move, the original object is left in a valid but unspecified state, so it should not be used after the move.

In conclusion, the ability to capture variables by move semantics in C++14 provides an improvement to lambda functions, allowing for more efficient and flexible code. By using the capture specifier `&&`, you can move objects into lambda functions instead of making copies or capturing by reference. This feature is particularly beneficial when working with large, non-copyable objects in C++.