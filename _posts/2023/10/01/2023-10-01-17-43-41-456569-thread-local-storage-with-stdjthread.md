---
layout: post
title: "Thread-local storage with `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

With the introduction of C++20, the Standard Library now includes the `std::jthread` class, which is an improvement over the traditional `std::thread` class for managing threads. One of the useful features offered by `std::jthread` is the ability to have thread-local storage.

Thread-local storage allows each thread to have its own copy of a variable, ensuring that each thread operates on its own independent instance. This can be particularly useful in scenarios where multiple threads need access to a shared resource but should not interfere with each other's data.

To use thread-local storage with `std::jthread`, you can leverage the `thread_local` keyword. The `thread_local` keyword allows you to declare variables that are specific to each thread.

```cpp
#include <iostream>
#include <thread>

thread_local int threadLocalCounter = 0;

void workerThread() {
    // Each thread will have its own instance of threadLocalCounter
    for (int i = 0; i < 5; ++i) {
        ++threadLocalCounter;
        std::cout << "Thread #" << std::this_thread::get_id() << ": " << threadLocalCounter << std::endl;
    }
}

int main() {
    std::jthread thread1(workerThread);
    std::jthread thread2(workerThread);

    thread1.join();
    thread2.join();

    return 0;
}
```

In the example above, we define a `thread_local` variable `threadLocalCounter` which keeps track of a counter specific to each thread. Each thread increments its own copy of the counter and prints the value along with the thread ID.

When the program is run, you will observe that each thread maintains its own counter and operates independently, without affecting each other's values.

Thread-local storage can be a powerful tool for managing concurrent access to shared resources in a multi-threaded environment. The use of `std::jthread` and the `thread_local` keyword in C++20 provides a convenient mechanism for achieving this task. It enables cleaner and more efficient management of thread-local variables, simplifying the development of concurrent applications.

#C++ #ThreadLocalStorage