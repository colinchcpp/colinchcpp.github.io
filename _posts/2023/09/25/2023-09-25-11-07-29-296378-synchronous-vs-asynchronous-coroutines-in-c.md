---
layout: post
title: "Synchronous vs asynchronous coroutines in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

In modern programming, coroutines are a powerful tool that provides more flexibility and efficiency in writing asynchronous code. They allow you to write code that runs asynchronously without the complexities of traditional callback-based approaches. C++ has introduced coroutines as part of the language standard to simplify asynchronous programming. However, there are two different flavors of coroutines - synchronous and asynchronous. Let's explore the differences between them.

Synchronous Coroutines:
Synchronous coroutines are similar to normal functions, where the execution flows from one statement to another in a sequential manner. When a coroutine is called, it starts executing and doesn't return until it completes its execution or until it hits a suspension point. A suspension point is a special keyword or statement that explicitly yields control back to the caller, allowing other tasks to be executed concurrently. 

Synchronous coroutines are useful when you want to write code that appears to be blocking but is actually executed asynchronously. The caller of the coroutine will wait for it to complete before proceeding to the next line of code.

Example:
```cpp
#include <iostream>
#include <coroutine>

std::coroutine_handle<> SimpleCoroutine()
{
    std::cout << "Coroutine started" << std::endl;
    co_yield {}; // Suspend coroutine execution
    std::cout << "Coroutine resumed" << std::endl;
    co_return; // Resume execution and complete the coroutine
}

int main()
{
    auto coroutine = SimpleCoroutine();
    coroutine.resume(); // Resume coroutine execution
    std::cout << "Main continues" << std::endl;
    return 0;
}
```

Output:
```
Coroutine started
Coroutine resumed
Main continues
```

Asynchronous Coroutines:
Asynchronous coroutines, on the other hand, are designed to work with operations that can take a significant amount of time, such as I/O operations or network requests. Unlike synchronous coroutines, asynchronous coroutines can suspend their execution without blocking the caller until the operation is completed. They allow other tasks to run while waiting for the operation to finish.

Asynchronous coroutines typically use `awaiter` objects to enable suspension and resumption of execution. These objects encapsulate the communication between the suspend/resume points. The underlying system handles the suspension of execution and notifies the coroutine to resume when the operation is completed.

Example:
```cpp
#include <iostream>
#include <experimental/coroutine>

struct Awaiter
{
    bool await_ready() const noexcept { return false; }
    void await_suspend(std::experimental::coroutine_handle<>) noexcept { /* Suspend coroutine and handle the async operation */ }
    void await_resume() noexcept { /* Resume coroutine after async operation completes */ }
};

std::experimental::suspend_always SimpleCoroutine()
{
    std::cout << "Coroutine started" << std::endl;
    co_await Awaiter{}; // Suspend coroutine and wait for the async operation to complete
    std::cout << "Coroutine resumed" << std::endl;
}

int main()
{
    auto coroutine = SimpleCoroutine();
    coroutine.resume();
    std::cout << "Main continues" << std::endl;
    return 0;
}
```

Output:
```
Coroutine started
Main continues
Coroutine resumed
```

Conclusion:
In summary, synchronous coroutines in C++ execute sequentially, blocking the caller until completion or suspension points are encountered. On the other hand, asynchronous coroutines allow for non-blocking execution, enabling the caller to continue with other tasks while waiting for the completion of asynchronous operations. Both styles of coroutines serve different purposes and can be utilized based on the specific requirements of your application.

#C++ #Coroutines