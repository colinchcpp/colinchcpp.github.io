---
layout: post
title: "Testing `std::jthread` code"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

With the release of C++20, a new addition to the Standard Library is the `std::jthread` class. `std::jthread` is a lightweight wrapper around `std::thread` that provides the ability to join or detach the underlying thread automatically when the `std::jthread` object goes out of scope. This can be useful in scenarios where you want to ensure proper thread management without explicit calls to `join` or `detach`.

Let's take a look at an example code snippet to demonstrate the usage of `std::jthread`:

```cpp
#include <iostream>
#include <thread>
#include <chrono>

void foo() {
    for (int i = 0; i < 5; ++i) {
        std::cout << "Executing foo: " << i << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(1));
    }
}

int main() {
    std::cout << "Main thread started" << std::endl;

    std::jthread t(foo);

    std::cout << "Main thread doing some work..." << std::endl;
    std::this_thread::sleep_for(std::chrono::seconds(3));

    std::cout << "Main thread finished" << std::endl;

    return 0;
}
```

In this example, we define a function `foo` that simply prints a message and waits for 1 second. We then create an instance of `std::jthread` named `t` that takes `foo` as its callable parameter. This means `foo` will be executed in a separate thread.

After creating the `std::jthread` object, the main thread carries on with some other work for 3 seconds before completing. When the `std::jthread` object `t` goes out of scope at the end of the `main` function, it automatically joins the underlying thread, ensuring that `foo` completes its execution before the program exits.

This automatic joining behavior of `std::jthread` eliminates the need for explicit calls to `join` or `detach`, making the code more concise and less error-prone.

Overall, `std::jthread` brings convenience and simplicity to thread management in C++ by providing automatic thread joining. It is a valuable addition to the Standard Library, making it easier to write clean and reliable multithreaded code.

#cplusplus #multithreading