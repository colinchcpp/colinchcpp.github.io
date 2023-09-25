---
layout: post
title: "Coroutine cancellation and cleanup in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Coroutines are a powerful feature in modern programming languages that allow developers to write asynchronous and concurrent code in an easy and intuitive manner. This paradigm is especially useful when dealing with tasks that involve I/O operations or long-running computations. However, one aspect that needs careful consideration is coroutine cancellation and cleanup.

## Cancellation of coroutines

Cancellation refers to the ability to stop the execution of a coroutine before it completes naturally. This can be useful in scenarios where a task becomes irrelevant or when the user explicitly requests to cancel the operation. In C++, cancellation can be achieved by throwing an exception from the coroutine, which can be caught and handled by the caller.

To implement cancellation in a coroutine, you can use the `std::cancel_token` class from the C++20 standard. This class represents a token that can be checked inside the coroutine to determine if a cancellation request has been made. Here's an example:

```cpp
#include <coroutine>
#include <exception>

struct cancellation_exception : std::exception {};

template<typename T>
struct cancellable_promise {
    T value;
    std::exception_ptr exception;
    std::coroutine_handle<> continuation;

    auto yield_value(T val) {
        value = val;
        return std::suspend_always{};
    }

    auto initial_suspend() { return std::suspend_always{}; }
    auto final_suspend() noexcept { return std::suspend_always{}; }

    void unhandled_exception() {
        exception = std::current_exception();
    }

    void return_void() {}
};

template<typename T>
struct cancellable_coroutine {
    std::coroutine_handle<cancellable_promise<T>> handle;

    cancellable_coroutine(std::coroutine_handle<cancellable_promise<T>> h) : handle(h) {}

    ~cancellable_coroutine() {
        if (handle) handle.destroy();
    }

    T get_result() {
        if (handle.promise().exception) {
            std::rethrow_exception(handle.promise().exception);
        }
        return handle.promise().value;
    }

    bool await_ready() { return false; }

    void await_suspend(std::coroutine_handle<> awaiting) {
        handle.promise().continuation = awaiting;
    }

    void await_resume() {}
};

template<typename T>
cancellable_coroutine<T> operator co_await(std::coroutine_handle<cancellable_promise<T>> handle) {
    return cancellable_coroutine<T>(handle);
}

cancellable_coroutine<int> my_coroutine(std::cancel_token cancel_token) {
    try {
        while (/*some condition*/) {
            // Perform some work

            if (cancel_token.is_cancellation_requested()) {
                throw cancellation_exception{};
            }

            // Resume the coroutine
            co_await std::suspend_always{};
        }
    } catch (const cancellation_exception&) {
    }
    
    co_return 42;
}

int main() {
    std::cancel_token_source cancel_source;
    auto cancel_token = cancel_source.get_token();

    cancellable_coroutine<int> coroutine_handle = my_coroutine(cancel_token);

    // Resume coroutine until completion or cancellation request
    while (!coroutine_handle.await_ready()) {
        coroutine_handle.await_resume();

        // Check if cancellation is requested
        if (cancel_token.is_cancellation_requested()) {
            cancel_token.throw_if_cancellation_requested();
        }
    }

    const int result = coroutine_handle.get_result();
    // Handle the result of the coroutine

    return 0;
}
```
In this example, the `cancellable_coroutine` class is used to wrap the coroutine handle and provide a convenient interface for resuming and checking for cancellation requests. The `cancellable_promise` struct is used as the promise type to handle the results and exceptions thrown from the coroutine.

## Cleanup of resources

Besides cancellation, it's also important to perform cleanup of any resources that were acquired during the execution of a coroutine. For example, if a coroutine opens a file or establishes a network connection, it should ensure that these resources are properly cleaned up when the coroutine is cancelled or completes.

One way to achieve resource cleanup is by using the RAII (Resource Acquisition Is Initialization) idiom. In C++, this is typically done through the use of smart pointers, such as `std::unique_ptr` or `std::shared_ptr`. By encapsulating the acquired resources in a smart pointer, the cleanup will be automatically handled when the pointer goes out of scope.

Here's an example demonstrating the use of `std::unique_ptr` for resource cleanup:

```cpp
#include <memory>
#include <iostream>

struct Resource {
    Resource() { std::cout << "Resource acquired\n"; }
    ~Resource() { std::cout << "Resource released\n"; }
};

std::unique_ptr<Resource> acquire_resource() {
    return std::make_unique<Resource>();
}

cancellable_coroutine<void> my_coroutine(std::cancel_token cancel_token) {
    auto resource = acquire_resource();

    try {
        while (/*some condition*/) {
            // Perform some work
            
            if (cancel_token.is_cancellation_requested()) {
                throw cancellation_exception{};
            }
            
            // Resume the coroutine
            co_await std::suspend_always{};
        }
    } catch (const cancellation_exception&) {
    }

    // Cleanup will be automatically handled when 'resource' goes out of scope

    co_return;
}

int main() {
    std::cancel_token_source cancel_source;
    auto cancel_token = cancel_source.get_token();

    cancellable_coroutine<void> coroutine_handle = my_coroutine(cancel_token);

    // Resume coroutine until completion or cancellation request
    while (!coroutine_handle.await_ready()) {
        coroutine_handle.await_resume();

        // Check if cancellation is requested
        if (cancel_token.is_cancellation_requested()) {
            cancel_token.throw_if_cancellation_requested();
        }
    }

    return 0;
}
```

In this example, the `acquire_resource` function returns a `std::unique_ptr<Resource>`, which ensures that the acquired resource is automatically released when the pointer goes out of scope. The cleanup is handled whether the coroutine completes normally or is cancelled.

By combining coroutine cancellation and proper cleanup techniques, developers can write efficient and robust asynchronous code that gracefully handles cancellation scenarios and resource management.