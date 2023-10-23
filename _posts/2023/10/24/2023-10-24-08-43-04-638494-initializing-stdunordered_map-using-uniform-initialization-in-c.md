---
layout: post
title: "Initializing std::unordered_map using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Uniform initialization provides a more concise and readable way to initialize containers and other objects by using a brace-enclosed initializer list. It is especially useful when initializing complex objects like `std::unordered_map`.

To initialize an `std::unordered_map` using uniform initialization, we can simply provide a list of key-value pairs enclosed in curly braces. Each key-value pair is specified using the syntax `key:value`. Here's an example:

```cpp
#include <unordered_map>
#include <iostream>

int main() {
  std::unordered_map<std::string, int> myMap = {
    {"apple", 5},
    {"banana", 3},
    {"orange", 8}
  };

  for (const auto& pair : myMap) {
    std::cout << pair.first << ": " << pair.second << std::endl;
  }

  return 0;
}
```

In the above example, we initialize an `std::unordered_map` named `myMap` with three key-value pairs. The keys are strings (`"apple"`, `"banana"`, `"orange"`) and the corresponding values are integers (`5`, `3`, `8`). We then iterate over the map and print each key-value pair.

Running the above code will output:

```
apple: 5
banana: 3
orange: 8
```

As you can see, we successfully initialized and accessed the elements of the `std::unordered_map` using uniform initialization.

Uniform initialization simplifies the process of initializing containers, making the code more readable and concise. It also provides an elegant way to initialize complex objects. It is important to note that uniform initialization is available in C++11 and later versions.

I hope this blog post helps you understand how to initialize an `std::unordered_map` using uniform initialization in C++. Happy coding!

References:
- [std::unordered_map - C++ Reference](https://en.cppreference.com/w/cpp/container/unordered_map)
- [Initializer List - C++ Reference](https://en.cppreference.com/w/cpp/utility/initializer_list)
- [Uniform Initialization - C++ Reference](https://en.cppreference.com/w/cpp/language/list_initialization)