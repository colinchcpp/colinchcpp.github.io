---
layout: post
title: "C++ concurrency models and synchronization primitives"
description: " "
date: 2023-10-16
tags: [concurrency]
comments: true
share: true
---

Concurrency is an essential aspect of modern software development, enabling programs to efficiently execute multiple tasks simultaneously. C++ provides various concurrency models and synchronization primitives to help developers write concurrent programs reliably and efficiently. In this blog post, we will explore some of these models and primitives.

## Table of Contents
- [Introduction to Concurrency](#introduction-to-concurrency)
- [Thread-based Concurrency](#thread-based-concurrency)
- [Task-based Concurrency](#task-based-concurrency)
- [Synchronization Primitives](#synchronization-primitives)
  - [Mutexes](#mutexes)
  - [Condition Variables](#condition-variables)
  - [Atomic Operations](#atomic-operations)
- [Conclusion](#conclusion)

## Introduction to Concurrency

Concurrency refers to the ability of a program to execute multiple tasks simultaneously, or in overlapping time intervals. It is particularly useful when dealing with I/O operations, CPU-intensive tasks, or improving overall system responsiveness. 

## Thread-based Concurrency

Threads are a fundamental unit of concurrency in C++. They represent independent paths of execution within a program. C++ provides the `std::thread` class, which allows developers to create and manage threads easily. By creating multiple threads, we can execute different parts of a program concurrently.

```cpp
#include <thread>

void SomeFunction()
{
    // Code to be executed by the thread
}

int main()
{
    std::thread myThread(SomeFunction);

    // Do other operations concurrently
    
    myThread.join();

    return 0;
}
```

## Task-based Concurrency

Task-based concurrency is an alternative model to thread-based concurrency. It focuses on dividing the program's work into smaller tasks, which can be executed concurrently by a task scheduler. C++ provides the `<future>` header with the `std::async` and `std::future` classes, which facilitate task-based concurrency.

```cpp
#include <future>

int SomeFunction()
{
    // Code to be executed by the task
    return 42;
}

int main()
{
    std::future<int> result = std::async(std::launch::async, SomeFunction);

    // Do other operations concurrently

    int value = result.get();

    return 0;
}
```

## Synchronization Primitives

When multiple threads or tasks access shared resources, synchronization is necessary to ensure data consistency and avoid race conditions. C++ provides several synchronization primitives for this purpose.

### Mutexes

Mutexes, short for mutual exclusion, are used to protect shared resources from being accessed simultaneously by multiple threads. C++ provides the `std::mutex` class for this purpose. A mutex can be locked and unlocked to create a critical section of code that only one thread can execute at a time.

```cpp
#include <mutex>

std::mutex mtx;

void SomeFunction()
{
    std::lock_guard<std::mutex> lock(mtx);

    // Code accessing the shared resource
}

int main()
{
    std::thread t1(SomeFunction);
    std::thread t2(SomeFunction);

    t1.join();
    t2.join();

    return 0;
}
```

### Condition Variables

Condition variables allow threads to efficiently wait for a certain condition to be met before continuing their execution. C++ provides the `std::condition_variable` class for this purpose. Threads can wait on a condition variable until another thread notifies them of a change in the condition.

```cpp
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
bool condition = false;

void WaitForCondition()
{
    std::unique_lock<std::mutex> lock(mtx);

    cv.wait(lock, []{ return condition; });

    // Code to execute after the condition is met
}

void NotifyCondition()
{
    std::lock_guard<std::mutex> lock(mtx);

    condition = true;
    cv.notify_one();
}

int main()
{
    std::thread t1(WaitForCondition);
    std::thread t2(NotifyCondition);

    t1.join();
    t2.join();

    return 0;
}
```

### Atomic Operations

Atomic operations ensure that certain operations on shared variables are performed atomically without interruption. C++ provides the `<atomic>` header with various atomic types, such as `std::atomic_int`, `std::atomic_bool`, etc. Atomic operations can be used to update shared variables without the need for locks.

```cpp
#include <atomic>

std::atomic_int counter(0);

void Increment()
{
    counter++;
}

int main()
{
    std::thread t1(Increment);
    std::thread t2(Increment);

    t1.join();
    t2.join();

    int result = counter;

    return 0;
}
```

## Conclusion

C++ provides various concurrency models and synchronization primitives to facilitate concurrent programming. Whether you prefer thread-based concurrency or task-based concurrency, or need to synchronize shared resources, C++ has you covered with its rich set of features. Understanding and utilizing these models and primitives can greatly enhance the performance and reliability of your concurrent programs.

**References:**
- [C++ Threads](https://en.cppreference.com/w/cpp/thread)
- [C++ Futures](https://en.cppreference.com/w/cpp/thread/future)
- [C++ Synchronization Primitives](https://en.cppreference.com/w/cpp/thread/sync_primitives)

#concurrency #C++