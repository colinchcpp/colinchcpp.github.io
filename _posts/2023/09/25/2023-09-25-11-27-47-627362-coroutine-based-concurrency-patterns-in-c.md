---
layout: post
title: "Coroutine-based concurrency patterns in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Concurrency is an essential concept in modern software development, enabling efficient utilization of resources and achieving responsive and scalable applications. Traditionally, threads have been the go-to mechanism for achieving concurrency in C++. However, with the introduction of coroutines in C++20, a new and more elegant approach to concurrency has emerged.

Coroutines enable developers to write asynchronous code that looks like synchronous code, making it easier to reason about and maintain. They provide a natural way to write code that executes concurrently without the need for explicit threading. In this blog post, we will explore some coroutine-based concurrency patterns in C++.

## Pattern 1: Asynchronous Execution

Asynchronous execution allows us to perform tasks concurrently without blocking the main thread. Coroutines make it easy to achieve asynchronous execution by providing mechanisms to suspend and resume execution at specific points.

```cpp
#include <iostream>
#include <experimental/coroutine>

// Asynchronous task
class AsyncTask {
public:
    struct promise_type {
        AsyncTask get_return_object() {
            return AsyncTask(std::experimental::coroutine_handle<promise_type>::from_promise(*this));
        }
        auto initial_suspend() { return std::experimental::suspend_never{}; }
        auto final_suspend() noexcept { return std::experimental::suspend_never{}; }
        void return_void() {}
    };

    AsyncTask(std::experimental::coroutine_handle<promise_type> handle)
        : handle(handle) {}

    ~AsyncTask() {
        if (handle)
            handle.destroy();
    }

    bool await_ready() { return false; }
    void await_suspend(std::experimental::coroutine_handle<> awaitingCoroutine) {
        handle.resume();
    }
    void await_resume() {}

private:
    std::experimental::coroutine_handle<promise_type> handle;
};

// Usage
AsyncTask asyncTask() {
    std::cout << "Starting async task." << std::endl;
    co_await std::experimental::suspend_always{};
    std::cout << "Async task resumed." << std::endl;
}

int main() {
    auto task = asyncTask();
    std::cout << "Main thread continues." << std::endl;
    return 0;
}
```

In this example, we define an `AsyncTask` class that represents an asynchronous task. The `promise_type` struct defines the coroutine promise type, which handles the coroutine's return value and control flow. We override the `initial_suspend()` and `final_suspend()` functions to ensure the coroutine never suspends. The `await_suspend()` function resumes the coroutine when awaited.

We then declare the `asyncTask()` function as a coroutine using the `co_await` keyword. Inside the coroutine, we print a message, suspend the coroutine, and then print another message. In the `main()` function, we create an instance of `asyncTask()` and continue executing on the main thread while the asynchronous task runs.

## Pattern 2: Parallel Execution

Parallel execution involves executing multiple tasks concurrently, leveraging the available processing power. Coroutines make parallel execution easier by providing a way to compose and coordinate multiple asynchronous tasks.

```cpp
#include <iostream>
#include <vector>
#include <experimental/coroutine>

// Asynchronous task
template<typename T>
class AsyncTask {
public:
    struct promise_type {
        AsyncTask get_return_object() {
            return AsyncTask(std::experimental::coroutine_handle<promise_type>::from_promise(*this));
        }
        auto initial_suspend() { return std::experimental::suspend_never{}; }
        auto final_suspend() noexcept { return std::experimental::suspend_always{}; }
        void return_value(T value) {
            result = value;
        }
        void unhandled_exception() {
            std::terminate();
        }
        T result;
    };

    AsyncTask(std::experimental::coroutine_handle<promise_type> handle)
        : handle(handle) {}

    ~AsyncTask() {
        if (handle)
            handle.destroy();
    }

    bool await_ready() { return false; }
    void await_suspend(std::experimental::coroutine_handle<> awaitingCoroutine) {
        handle.resume();
    }
    T await_resume() {
        return handle.promise().result;
    }

private:
    std::experimental::coroutine_handle<promise_type> handle;
};

// Usage
AsyncTask<int> asyncTask(int id) {
    std::cout << "Starting task " << id << std::endl;
    co_await std::experimental::suspend_always{};
    std::cout << "Task " << id << " completed." << std::endl;
    co_return id;
}

int main() {
    std::vector<AsyncTask<int>> tasks;
    for (int i = 0; i < 5; ++i) {
        tasks.push_back(asyncTask(i));
    }
    for (auto& task : tasks) {
        std::cout << "Task result: " << task.await_resume() << std::endl;
    }
    return 0;
}
```

In this example, we define a template class `AsyncTask` that represents an asynchronous task. The promise type is specialized with the desired return type. The coroutine suspends at the `co_await` point and resumes when awaited.

We create a vector of `AsyncTask<int>` to hold multiple tasks. Each task executes concurrently and returns its id. We then iterate over the tasks and print their results.

Coroutines provide an expressive way to implement parallel execution, taking advantage of the underlying concurrency mechanisms while providing a more readable and flexible code structure.

## Conclusion

Using coroutines, we can harness the power of asynchronous and parallel execution in C++ without heavily relying on traditional threading mechanisms. The examples presented in this blog post demonstrate how coroutines can simplify the implementation of concurrency patterns. By leveraging coroutines and their concise syntax, C++ developers can write more readable and maintainable code while achieving efficient and scalable concurrency.

#cpp #coroutines