---
layout: post
title: "Moving `std::unique_ptr` between threads"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

When working with multi-threaded code in C++, it is essential to ensure proper ownership and transfer of resources between threads. The `std::unique_ptr` template class provided by the C++ Standard Library is a powerful smart pointer that can be used to manage dynamically allocated resources and automatically deallocate them when they are no longer needed. 

However, `std::unique_ptr` cannot be copied, only moved, because it encapsulates sole ownership of the managed object. When it comes to transferring ownership between threads, there are a few considerations to keep in mind to avoid data races or undefined behavior. 

Here's an example of how to correctly move a `std::unique_ptr` between threads:

```cpp
#include <iostream>
#include <memory>
#include <thread>

void threadFunc(std::unique_ptr<int> ptr) {
    // Use the resource managed by the unique_ptr in the new thread
    std::cout << "Value in new thread: " << *ptr << std::endl;
}

int main() {
    std::unique_ptr<int> ptr(new int(42));

    // Create a new thread and pass the unique_ptr by moving it
    std::thread t(threadFunc, std::move(ptr));

    // Wait for the thread to finish
    t.join();

    // Here, `ptr` no longer points to a valid object as ownership was transferred
    // to the new thread

    return 0;
}
```

In the `main` function, we create a `std::unique_ptr` named `ptr` that manages an `int` object. To pass `ptr` to the new thread, we use `std::move` to transfer ownership of the managed object to the thread function `threadFunc`. The `std::move` function casts `ptr` to an rvalue reference, enabling move semantics. 

In the `threadFunc`, we can safely access and use the object managed by the `unique_ptr`. In this example, we simply print the value to the console. 

It's important to note that once the ownership is transferred, the original `ptr` in the `main` function no longer points to a valid object. You should refrain from using it further to avoid any potential issues.

Remember to include the `<memory>` and `<thread>` headers for proper usage of `std::unique_ptr` and `std::thread`. Additionally, ensure that proper synchronization mechanisms, such as mutexes or condition variables, are in place when necessary to avoid data races or other concurrency issues.

#cpp #multithreading #smartpointers