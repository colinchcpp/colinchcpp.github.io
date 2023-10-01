---
layout: post
title: "Memory visibility and memory coherency in C++."
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

In concurrent programming, ensuring proper memory visibility and memory coherency is crucial to write correct and predictable code. This is true not just in C++, but in most programming languages. In this blog post, we will explore what memory visibility and memory coherency mean and how they are handled in C++.

## Memory Visibility

Memory visibility is the concept of how changes made to a particular memory location in one thread become visible to other threads. In other words, it determines when changes made by one thread become visible to another thread that reads the same memory location. In C++, there are three main ways to achieve memory visibility:

1. **Sequential Consistency**: This is the default memory model in C++. Operations in a program appear to be executed in a strict sequential order, regardless of the number of threads involved. With sequential consistency, reads and writes have a total order.

2. **Acquire-Release Semantics**: This is a more relaxed memory model compared to sequential consistency. It allows for reordering of certain memory operations, but enforces ordering on critical points where synchronization is required. Acquire semantics ensure that all previous memory operations become visible to subsequent reads or writes, while release semantics guarantee that all subsequent memory operations become visible to preceding reads or writes.

3. **Relaxed Memory Ordering**: Relaxed memory ordering provides the most flexibility and allows for the greatest degree of reordering. It allows for reordering of both relaxed and non-relaxed memory operations. However, it does not provide any synchronization or guarantees about the order of memory operations.

## Memory Coherency

Memory coherency deals with the consistency of shared data across multiple processors or cores in a system. In a multi-threaded or multi-core environment, each thread or core may have its own cache, and changes made by one thread may not be immediately reflected in the caches of other threads. C++ provides several mechanisms to ensure memory coherency:

1. **Mutexes and Locks**: Mutexes and locks are synchronization primitives that ensure exclusive access to shared resources. By locking a mutex before accessing a shared variable, memory coherency is guaranteed, as acquiring the lock ensures that all previous memory operations are visible to the thread.

Example code using mutex:

```cpp
#include <iostream>
#include <mutex>

std::mutex mtx;
int sharedVariable = 0;

void incrementSharedVariable()
{
    std::lock_guard<std::mutex> lock(mtx);
    sharedVariable++;
}

int main()
{
    std::thread t1(incrementSharedVariable);
    std::thread t2(incrementSharedVariable);

    t1.join();
    t2.join();

    std::cout << "Shared Variable: " << sharedVariable << std::endl;

    return 0;
}
```

2. **Atomic Operations**: C++ provides atomic types and operations that ensure indivisible access to shared variables. Atomic operations guarantee memory coherency without the need for explicit locking. They are typically more efficient than using locks, as they avoid the overhead of acquiring and releasing locks.

Example code using atomic:

```cpp
#include <iostream>
#include <atomic>

std::atomic<int> sharedVariable(0);

void incrementSharedVariable()
{
    sharedVariable++;
}

int main()
{
    std::thread t1(incrementSharedVariable);
    std::thread t2(incrementSharedVariable);

    t1.join();
    t2.join();

    std::cout << "Shared Variable: " << sharedVariable << std::endl;

    return 0;
}
```

## Conclusion

Memory visibility and memory coherency are essential concepts to understand when writing concurrent code in C++. By properly managing memory access and synchronization, we can ensure correct and predictable behavior of our programs. Whether using mutexes and locks or atomic operations, choosing the right synchronization mechanism depends on the specific requirements of the application. With a solid understanding of these concepts, you can avoid common concurrency issues and build robust concurrent applications.

#programming #concurrency