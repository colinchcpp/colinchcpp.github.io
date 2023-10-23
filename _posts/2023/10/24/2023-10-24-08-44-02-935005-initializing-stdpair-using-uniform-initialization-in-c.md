---
layout: post
title: "Initializing std::pair using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

```cpp
#include <iostream>
#include <utility>

int main() {
    // Using uniform initialization to initialize a std::pair
    auto pair = std::pair<int, std::string>{42, "Hello World"};

    // Accessing the elements of the pair
    std::cout << "First element: " << pair.first << std::endl;
    std::cout << "Second element: " << pair.second << std::endl;

    return 0;
}
```

In the code snippet above, we include the necessary headers `<iostream>` for outputting the values and `<utility>` for using `std::pair`. Inside the `main()` function, we declare a variable `pair` and initialize it using uniform initialization syntax.

The type of the pair elements is specified between angle brackets `< >`. In this example, we have an `int` as the first element and a `std::string` as the second element.

To access the individual elements of the pair, we use the `.first` and `.second` member variables. In this case, we use `std::cout` to print the values of the elements.

When you run this code, you will see the output:

```
First element: 42
Second element: Hello World
```

By using uniform initialization syntax, you can easily initialize `std::pair` objects in a concise and readable way.