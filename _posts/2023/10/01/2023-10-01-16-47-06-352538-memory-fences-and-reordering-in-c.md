---
layout: post
title: "Memory fences and reordering in C++."
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

In a multi-threaded environment, memory fences and reordering play a crucial role in ensuring the correctness of concurrent programs. C++ provides mechanisms to control memory ordering and prevent undesired reordering of instructions. In this blog post, we will explore memory fences and their impact on instruction reordering in C++.

## Understanding Memory Reordering

Memory reordering occurs when the compiler or the processor changes the order of instructions during program execution. This optimization technique aims to improve performance by rearranging instructions for better hardware utilization. However, in multi-threaded programs, memory reordering can lead to unexpected results and violate the intended program semantics.

Consider the following example:

```cpp
#include <atomic>
#include <iostream>
#include <thread>

std::atomic<int> x = 0;
std::atomic<int> y = 0;

void ThreadA()
{
    y.store(1, std::memory_order_relaxed);
    x.store(2, std::memory_order_relaxed);
}

void ThreadB()
{
    while (x.load(std::memory_order_relaxed) != 2);
    std::cout << "Value of y: " << y.load(std::memory_order_relaxed) << std::endl;
}

int main()
{
    std::thread thread1(ThreadA);
    std::thread thread2(ThreadB);

    thread1.join();
    thread2.join();

    return 0;
}
```

In this code, `ThreadA` sets `y` to 1 and `x` to 2, both with `std::memory_order_relaxed`. Meanwhile, `ThreadB` enters a busy-wait loop until `x` is set to 2. Once `x` reaches the expected value, it prints the value of `y`. 

At first glance, one might expect the output to always be 1, since `y` is assigned before `x` in `ThreadA`. However, due to memory reordering, there is no guarantee that the instructions will be executed in the same order as they appear in the code.

## Introducing Memory Fences

A memory fence is a synchronization primitive that ensures that certain memory operations are completed before or after others. It acts as a barrier that separates the instructions that come before from those that come after it. In C++, memory fences are achieved using memory orderings and the `std::atomic_thread_fence` function.

By modifying our previous example to include memory fences, we can ensure the desired ordering of memory operations:

```cpp
#include <atomic>
#include <iostream>
#include <thread>

std::atomic<int> x = 0;
std::atomic<int> y = 0;

void ThreadA()
{
    y.store(1, std::memory_order_relaxed);
    std::atomic_thread_fence(std::memory_order_release);
    x.store(2, std::memory_order_relaxed);
}

void ThreadB()
{
    while (x.load(std::memory_order_relaxed) != 2);
    std::atomic_thread_fence(std::memory_order_acquire);
    std::cout << "Value of y: " << y.load(std::memory_order_relaxed) << std::endl;
}

int main()
{
    std::thread thread1(ThreadA);
    std::thread thread2(ThreadB);

    thread1.join();
    thread2.join();

    return 0;
}
```

In this updated code, we have added memory fences using `std::atomic_thread_fence`. In `ThreadA`, the `std::memory_order_release` fence ensures that all preceding memory operations are completed before the fence. In `ThreadB`, the `std::memory_order_acquire` fence guarantees that all subsequent memory operations are completed after the fence.

With memory fences in place, the output of the program will always be 1, as intended. The memory fences effectively prevent any undesired reordering of memory operations.

## Conclusion

Understanding memory fences and reordering is crucial in writing correct and efficient multi-threaded code in C++. Memory fences provide the necessary synchronization primitives to maintain the desired order of memory operations. By using appropriate memory orderings and memory fences, one can ensure the correctness of concurrent programs and avoid race conditions.

#programming #concurrency