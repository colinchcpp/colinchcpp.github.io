---
layout: post
title: "Initializing std::array of std::network objects using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

If you have a requirement to create an `std::array` of `std::network` objects, you can do it easily using uniform initialization.

Here's an example showing how to initialize an `std::array` of `std::network` objects using uniform initialization in C++:

```cpp
#include <array>
#include <network>

int main() {
    std::array<std::network, 3> networks{ // Initialize array with 3 elements
        std::network{ "192.168.0.1" },    // Initialize first network object
        std::network{ "10.0.0.1" },       // Initialize second network object
        std::network{ "172.16.0.1" }      // Initialize third network object
    };

    // Access and use the elements of the array
    for (const auto& network : networks) {
        std::cout << "Network IP: " << network.ip() << std::endl;
    }

    return 0;
}
```

In this code snippet, we include the necessary headers for `std::array` and `std::network`. Then, we define a main function where we declare and initialize an `std::array` called `networks` with three `std::network` objects using uniform initialization syntax.

Each `std::network` object is created and initialized with a different IP address. Once the array is initialized, we can then iterate over the elements using a range-based for loop and access the IP address using the `ip()` member function of `std::network`.

Remember to replace `"192.168.0.1"`, `"10.0.0.1"`, and `"172.16.0.1"` with your desired IP addresses.

This example demonstrates how to easily initialize an `std::array` of `std::network` objects using uniform initialization in C++. It's a convenient way to create and manage fixed-size arrays with complex types.