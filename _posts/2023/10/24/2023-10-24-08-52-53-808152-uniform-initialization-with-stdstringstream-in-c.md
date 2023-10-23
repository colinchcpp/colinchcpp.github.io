---
layout: post
title: "Uniform initialization with std::stringstream in C++"
description: " "
date: 2023-10-24
tags: [uniform]
comments: true
share: true
---

In modern C++, uniform initialization is a convenient way to initialize objects, including standard library types. One such type is `std::stringstream` which provides a flexible way to work with strings as streams. In this blog post, we will explore how to initialize and use `std::stringstream` using uniform initialization.

## Initialization of `std::stringstream` Using Uniform Initialization

Prior to C++11, `std::stringstream` had to be initialized using the constructor. However, with the introduction of uniform initialization, we can now initialize `std::stringstream` objects more easily and concisely.

```cpp
#include <sstream>

int main() {
    // Initializing std::stringstream using uniform initialization
    std::stringstream ss{"Hello, World!"};

    // Rest of the code here...

    return 0;
}
```

In the above code snippet, we create a `std::stringstream` object named `ss` and initialize it with the string `"Hello, World!"` using uniform initialization.

## Using `std::stringstream` object

Once we have initialized the `std::stringstream` object, we can use it to perform various operations on strings, such as extracting data or manipulating the contents. Here is a simple example:

```cpp
#include <iostream>
#include <sstream>

int main() {
    std::stringstream ss{"C++ is great!"};

    std::string word;
    while (ss >> word) {
        std::cout << word << std::endl;
    }

    return 0;
}
```

The code snippet above demonstrates how to extract individual words from the `std::stringstream` object `ss` and then print them. The `ss >> word` statement extracts words from the stream one-by-one until all the words have been retrieved.

## Conclusion

Uniform initialization in C++ provides a cleaner and more concise way to initialize standard library types, such as `std::stringstream`. By leveraging uniform initialization, we can easily initialize `std::stringstream` objects with strings and perform various operations on them.

Using uniform initialization not only improves code readability but also aligns with the modern C++ coding style. It is recommended to use uniform initialization whenever possible in order to write more expressive and maintainable code.

Hashtags: #C++ #uniform-initialization