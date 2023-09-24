---
layout: post
title: "Atomic operations and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

In multithreaded programming, it is crucial to ensure that shared resources are accessed and modified safely to prevent data races and undefined behavior. One way to achieve this is by using atomic operations and smart pointers like `std::shared_ptr` in C++.

## Atomic Operations

Atomic operations guarantee that a variable can be safely accessed and modified by multiple threads without causing data corruption or race conditions. The C++ standard library provides atomic types, such as `std::atomic`, that allow operations on shared variables to be performed atomically.

For example, consider a counter that needs to be incremented by multiple threads concurrently:

```cpp
#include <iostream>
#include <atomic>
#include <thread>

std::atomic<int> counter(0);

void incrementCounter(int numIterations) {
    for (int i = 0; i < numIterations; ++i) {
        counter.fetch_add(1, std::memory_order_relaxed);
    }
}

int main() {
    constexpr int numThreads = 4;
    constexpr int numIterationsPerThread = 100000;

    std::thread threads[numThreads];

    for (int i = 0; i < numThreads; ++i) {
        threads[i] = std::thread(incrementCounter, numIterationsPerThread);
    }

    for (int i = 0; i < numThreads; ++i) {
        threads[i].join();
    }

    std::cout << "Counter value: " << counter.load() << std::endl;

    return 0;
}
```

In this example, the `std::atomic<int>` type is used to ensure that the counter is incremented atomically by multiple threads. The `fetch_add` member function adds the specified value to the counter in an atomic manner, allowing concurrent access without data races. The `std::memory_order_relaxed` argument specifies the memory ordering constraints for the atomic operation.

## `std::shared_ptr`

`std::shared_ptr` is a smart pointer that provides shared ownership of an object. It ensures that the object remains alive as long as there are references to it. `std::shared_ptr` implements a form of reference counting, where the object is deleted when the last shared pointer referencing it goes out of scope.

The atomic operations can be combined with `std::shared_ptr` to safely modify and access shared resources in a multithreaded environment. For example, imagine a scenario where multiple threads need to access a shared resource represented by a `sharedData` object:

```cpp
#include <iostream>
#include <atomic>
#include <thread>
#include <memory>

struct SharedData {
    std::string data;
    // ...
};

std::shared_ptr<SharedData> sharedData = std::make_shared<SharedData>();

void updateSharedData() {
    std::shared_ptr<SharedData> localData = std::atomic_load(&sharedData);  // Atomic load

    // Perform some operations on localData
    // ...

    std::atomic_store(&sharedData, localData);  // Atomic store
}

int main() {
    constexpr int numThreads = 4;

    std::thread threads[numThreads];

    for (int i = 0; i < numThreads; ++i) {
        threads[i] = std::thread(updateSharedData);
    }

    for (int i = 0; i < numThreads; ++i) {
        threads[i].join();
    }

    // Access sharedData
    std::shared_ptr<SharedData> finalData = std::atomic_load(&sharedData);
    std::cout << "Shared data: " << finalData->data << std::endl;

    return 0;
}
```

In this example, `std::atomic_load` and `std::atomic_store` are used to safely access and modify the `sharedData` object. The `std::atomic_load` function ensures that the current state of `sharedData` is safely loaded without any race conditions, and `std::atomic_store` updates the `sharedData` with the modified local copy.

By combining atomic operations with `std::shared_ptr`, you can safely manage shared resources in a multithreaded environment, ensuring thread-safety and preventing data races.

#tech #multithreading