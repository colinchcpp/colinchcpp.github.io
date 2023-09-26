---
layout: post
title: "Coroutine cancellation vs interruption in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Coroutines are becoming increasingly popular in modern C++ programming due to their ability to simplify asynchronous code. However, when it comes to cancelling or interrupting coroutines, there is often confusion around the terminology and the best practices. In this blog post, we will explore the differences between coroutine cancellation and interruption in C++ and discuss when to use each approach.

## Coroutine Cancellation

Coroutine cancellation refers to the process of terminating a running coroutine prematurely. This can be useful in scenarios where the coroutine is taking too long to complete, or when the result is no longer needed. Cancellation allows us to free up system resources and avoid wasting unnecessary computation.

In C++, coroutine cancellation is typically achieved using a cancellation token. The cancellation token is a boolean flag that can be observed by the coroutine, and when set to true, the coroutine can gracefully terminate its execution. The cancellation token can be passed as an argument to the coroutine function or stored as a member variable within the coroutine object.

Here's an example of how coroutine cancellation can be implemented using a cancellation token in C++20:

```cpp
#include <coroutine>
#include <iostream>

struct CancellationToken {
    bool cancelled = false;
};

struct Coroutine {
    CancellationToken* token;

    coroutine_handle<> handle;

    Coroutine(CancellationToken* token) : token(token) {}

    void operator()() {
        while (!token->cancelled) {
            std::cout << "Coroutine is running\n";
            // Coroutine logic goes here
            std::cout << "Coroutine iteration complete\n";
            // Coroutine logic goes here
        }
        std::cout << "Coroutine cancelled\n";
        handle.destroy();
    }
};

int main() {
    CancellationToken token;
    Coroutine coroutine(&token);
    coroutine.handle = coroutine.operator()().address();
    // ... Run the coroutine

    token.cancelled = true;
    // ... Cancel the coroutine
}
```

In this example, the `CancellationToken` is used to control the cancellation of the `Coroutine`. When the `cancelled` flag is set to true, the coroutine exits gracefully.

## Coroutine Interruption

Coroutine interruption, on the other hand, is a technique where an external entity interrupts the execution of a coroutine, but without terminating it outright. Interrupting a coroutine allows us to perform some actions or react to certain events while the coroutine is running.

In C++, coroutine interruption is typically achieved using the `std::experimental::coroutine_handle` and the `resume()` function. By calling the `resume()` function on a coroutine handle, we can interrupt the execution of the coroutine at specific points and perform desired operations. The coroutine can then be resumed using the `resume()` function again.

Here's an example that demonstrates coroutine interruption in C++20:

```cpp
#include <coroutine>
#include <iostream>

struct Coroutine {
    std::experimental::coroutine_handle<> handle;

    void operator()() {
        std::cout << "Coroutine started\n";
        std::cout << "Coroutine is running\n";
        // Coroutine logic goes here
        std::cout << "Coroutine interrupted\n";
        handle.resume();
        std::cout << "Coroutine resumed\n";
        // Coroutine logic goes here
        std::cout << "Coroutine completed\n";
        handle.destroy();
    }
};

int main() {
    Coroutine coroutine;
    coroutine.handle = coroutine.operator()().address();
    // ... Run the coroutine

    coroutine.handle.resume();
    // ... Interrupt the coroutine

    // ... Resume the coroutine
}
```

In this example, the `Coroutine` is interrupted after the first part of its logic is executed. The `resume()` function is called on the coroutine handle to interrupt the coroutine and then resume it at a later point.

## Conclusion

Coroutine cancellation and interruption are both useful techniques in C++ when dealing with coroutines. Understanding the differences between the two and knowing when to use each can greatly improve the design and efficiency of your asynchronous code. Cancellation is suitable for terminating the coroutine, while interruption allows for controlled pausing and resuming of its execution. By leveraging these concepts effectively, you can write more robust and flexible coroutines in your C++ programs. 

## #C++ #Coroutines