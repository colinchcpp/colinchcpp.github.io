---
layout: post
title: "Flushing output streams in C++"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

In C++, the `std::cout` and `std::cerr` are commonly used for printing output to the console. However, by default, these streams are **buffered**, which means that the output is not immediately printed to the console. Instead, it is stored in a buffer and only displayed when certain conditions are met.

There are cases when you may want to force the immediate display of output on the console, such as printing progress updates or debugging information. This can be achieved by **flushing** the output streams.

## Flushing the std::cout stream

To flush the `std::cout` stream, you can use the `std::flush` manipulator or the `std::endl` manipulator.

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, world!" << std::flush;
    // or
    // std::cout << "Hello, world!" << std::endl;

    return 0;
}
```

The `std::flush` manipulator flushes the output stream, forcing the immediate display of the contents in the buffer. Alternatively, you can use the `std::endl` manipulator, which not only flushes the stream but also inserts a newline character.

## Flushing the std::cerr stream

The `std::cerr` stream is typically used for printing error messages and is already **unbuffered**, meaning that it does not have an internal buffer. As a result, any output sent to `std::cerr` is immediately displayed on the console.

However, if you want to explicitly flush `std::cerr`, you can also use the `std::flush` manipulator or the `std::endl` manipulator.

```cpp
#include <iostream>

int main() {
    std::cerr << "Error: Something went wrong!" << std::flush;
    // or
    // std::cerr << "Error: Something went wrong!" << std::endl;

    return 0;
}
```

## Conclusion

Flushing the output streams can be useful in situations where you want to ensure immediate display of the output on the console. In this blog post, we learned how to flush the `std::cout` and `std::cerr` streams using the `std::flush` and `std::endl` manipulators in C++. Don't forget to leverage these methods when needed to improve your debugging or progress reporting capabilities.

#C++ #outputstreams #flush