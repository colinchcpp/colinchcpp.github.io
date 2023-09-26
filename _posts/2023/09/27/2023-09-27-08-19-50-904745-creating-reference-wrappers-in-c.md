---
layout: post
title: "Creating reference wrappers in C++"
description: " "
date: 2023-09-27
tags: [programming, cplusplus]
comments: true
share: true
---

In C++, reference wrappers provide a way to store and pass references as regular objects. They act as a non-owning reference to an object, allowing you to use references in situations where references are not possible, such as in containers like vectors and maps.

Reference wrappers are implemented using the `std::reference_wrapper` class, provided by the C++ Standard Library. To use reference wrappers, you need to include the `<functional>` header.

Here's an example that demonstrates how to create and use reference wrappers:

```cpp
#include <iostream>
#include <functional>
#include <vector>

void increment(int& value) {
    value++;
}

int main() {
    int num1 = 10;
    int num2 = 20;

    std::vector<std::reference_wrapper<int>> numbers{num1, num2};

    for (auto& num : numbers) {
        increment(num);
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the code above, we define a function `increment` that takes an integer reference and increments its value by one. We then create two integer variables `num1` and `num2`. 

Next, we create a vector `numbers` of reference wrappers for integers and initialize it with `num1` and `num2`. This allows us to store references to `num1` and `num2` in the vector.

Finally, we iterate over the vector using a range-based for loop. Since `numbers` stores reference wrappers, we can pass them to the `increment` function as regular references. After incrementing each value, we print it out to the console.

When you run the program, it will output `11 21`, indicating that the values of `num1` and `num2` were successfully incremented through the reference wrappers.

By using reference wrappers, you can effectively store and use references in containers and other situations where references are not directly supported. This provides additional flexibility and convenience in your C++ code.

#programming #cplusplus