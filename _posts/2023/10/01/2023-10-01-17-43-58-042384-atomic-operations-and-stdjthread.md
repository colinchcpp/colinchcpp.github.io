---
layout: post
title: "Atomic operations and `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

Atomic operations guarantee that the operations appear indivisible and are never interleaved with other atomic operations or non-atomic operations. This ensures that data integrity is maintained, avoiding race conditions or data corruption. Atomic operations are typically much faster and lighter than traditional locking mechanisms, making them a great choice for high-performance applications.

To perform atomic operations, the C++ `<atomic>` library provides various atomic types, such as `std::atomic`, `std::atomic_int`, `std::atomic_bool`, etc. These types allow you to perform atomic read-modify-write operations, such as increment, decrement, exchange, compare-and-swap, and more.

Let's take a look at an example where `std::atomic_int` is used to increment a shared counter in a multi-threaded environment:

```cpp
#include <atomic>
#include <iostream>
#include <thread>

std::atomic_int counter(0);

void incrementCounter(int numIterations) {
    for (int i = 0; i < numIterations; ++i) {
        counter.fetch_add(1, std::memory_order_relaxed);
    }
}

int main() {
    constexpr int NumThreads = 4;
    constexpr int NumIterations = 1000000;
    std::thread threads[NumThreads];

    for (int i = 0; i < NumThreads; ++i) {
        threads[i] = std::thread(incrementCounter, NumIterations);
    }

    for (int i = 0; i < NumThreads; ++i) {
        threads[i].join();
    }

    std::cout << "Counter value: " << counter << std::endl;

    return 0;
}
```

In the above code, we create an atomic integer variable `counter` and initialize it to 0. Each thread increments the counter a certain number of times using the `fetch_add` function, which performs an atomic addition. Finally, we join all the threads and print the final value of the counter.

With atomic operations, we can safely manipulate shared data without worrying about race conditions or data corruption. It is important to choose the appropriate atomic operation and memory ordering based on the specific requirements of your application.

#cpp #concurrency

---

By utilizing the new `<atomic>` library in C++, you can easily perform atomic operations on shared data in a thread-safe manner. This not only ensures data integrity and synchronization but also improves the performance of your multi-threaded applications.

One important addition in C++20 is the introduction of `std::jthread`, which is a new class for managing threads. `std::jthread` acts as a high-level wrapper around `std::thread` and provides additional features such as automatic joining and interruption.

Let's see an example of how `std::jthread` can be used:

```cpp
#include <iostream>
#include <chrono>
#include <thread>

void workerFunction() {
    std::cout << "Worker thread started.\n";
    std::this_thread::sleep_for(std::chrono::seconds(3));
    std::cout << "Worker thread finished.\n";
}

int main() {
    std::cout << "Main thread started.\n";

    std::jthread workerThread(workerFunction);
    std::this_thread::sleep_for(std::chrono::seconds(1));
    
    // After 1 second, request the thread to stop execution.
    workerThread.request_stop();

    std::cout << "Main thread finished.\n";

    return 0;
}
```

In this code, we have a `workerFunction` that simulates some work being done on a worker thread. The main thread creates a `std::jthread` and passes the `workerFunction` as a callable object to be executed by the new thread. After 1 second, the main thread requests the worker thread to stop by calling `request_stop()` on the `std::jthread` object.

`std::jthread` automatically joins the thread when the `std::jthread` object is destroyed. This means that we don't need to explicitly call `join()` or `detach()` on the thread object, making it convenient and preventing resource leaks.

Additionally, `std::jthread` supports interruption, allowing one thread to request another thread to stop its execution. This can be useful for gracefully stopping threads in response to some event or condition.

Using `std::jthread` simplifies the management of threads in C++, making it easier to write robust and efficient multi-threaded code.

#cpp #multi-threading