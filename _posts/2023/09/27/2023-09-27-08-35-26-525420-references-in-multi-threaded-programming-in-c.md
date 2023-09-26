---
layout: post
title: "References in multi-threaded programming in C++"
description: " "
date: 2023-09-27
tags: [multi]
comments: true
share: true
---

Multi-threaded programming in C++ allows developers to create programs that can perform multiple tasks concurrently. It is a powerful feature that enables efficient utilization of system resources and can greatly enhance the performance of applications. However, it also introduces new challenges and complexities that developers need to be aware of.

In this blog post, we will explore the basics of multi-threaded programming in C++, covering topics such as thread creation, synchronization, and common pitfalls to avoid.

## 1. Thread Creation

Creating a thread in C++ involves a few steps. First, you need to include the `<thread>` header file, which provides the necessary functions and classes for working with threads. Then, you can create a thread by calling the `std::thread` constructor and passing a callable object or a function pointer as an argument.

```cpp
#include <iostream>
#include <thread>

void myFunction() {
    // Code executed by the new thread
    std::cout << "Hello from a thread!" << std::endl;
}

int main() {
    // Create a new thread
    std::thread t(myFunction);

    // Do other work in the main thread

    // Wait for the thread to finish
    t.join();

    return 0;
}
```

In the example above, we define a function `myFunction` that will be executed by the new thread. We create a thread `t` and pass `myFunction` as an argument to the `std::thread` constructor. Finally, we call `t.join()` to wait for the thread to finish before exiting the program. Without the `join()` call, the main thread would terminate immediately, prematurely ending the execution of the new thread.

## 2. Synchronization

When working with multiple threads, synchronization becomes crucial to avoid race conditions and ensure data consistency. C++ provides various synchronization primitives, such as mutexes, condition variables, and atomic operations, to handle these scenarios.

### Mutexes

A mutex is a mutual exclusion object that allows only one thread to access a shared resource at a time. Threads can acquire a lock on a mutex using the `std::mutex` class. This ensures that only one thread can execute a critical section of code protected by the mutex.

```cpp
#include <iostream>
#include <mutex>
#include <thread>

std::mutex mtx;

void myFunction() {
    std::lock_guard<std::mutex> lock(mtx); // Lock the mutex

    // Code executed in the critical section

    // Mutex is automatically released when lock goes out of scope
}

int main() {
    std::thread t1(myFunction);
    std::thread t2(myFunction);

    t1.join();
    t2.join();

    return 0;
}
```

In the above example, we create two threads `t1` and `t2` that both call `myFunction`. Inside `myFunction`, we use a `std::lock_guard` to acquire a lock on the mutex `mtx`. This ensures that only one thread can execute the critical section of code at a time.

### Condition Variables

Condition variables enable threads to wait for certain conditions to be satisfied before proceeding. They are often used in conjunction with mutexes to build more complex synchronization mechanisms.

```cpp
#include <iostream>
#include <mutex>
#include <condition_variable>
#include <thread>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void myFunction() {
    std::unique_lock<std::mutex> lock(mtx); // Lock the mutex

    // Wait until ready flag is set
    cv.wait(lock, [] { return ready; });

    // Code executed after the condition is satisfied
}

int main() {
    std::thread t1(myFunction);

    // Do some work...

    // Set the ready flag
    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true;
    }

    cv.notify_one(); // Notify the waiting thread

    t1.join();

    return 0;
}
```

In the above example, the thread `t1` waits until the `ready` flag is set before proceeding. Inside `myFunction`, we use a `std::unique_lock` to acquire a lock on the mutex `mtx`, and then call `cv.wait` to wait until the condition is satisfied. The `cv.notify_one()` call is used to wake up the waiting thread once the condition is met.

## Conclusion

Multi-threaded programming in C++ allows for concurrent execution of tasks, improving application performance. By understanding thread creation, synchronization techniques, and avoiding common pitfalls, developers can harness the power of multi-threading to build efficient and responsive applications.

To explore more advanced topics in multi-threaded programming in C++, consider referring to the following resources:
- Threading in C++ - [link](https://www.learncpp.com/cpp-tutorial/mutex-and-unique_lock-part-1/)
- C++ Concurrency in Action by Anthony Williams - [link](https://www.manning.com/books/c-plus-plus-concurrency-in-action-second-edition)

#C++ #multi-threading