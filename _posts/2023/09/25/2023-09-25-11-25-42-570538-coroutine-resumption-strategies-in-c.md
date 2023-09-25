---
layout: post
title: "Coroutine resumption strategies in C++"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

## Introduction

Coroutines are a powerful feature in modern programming languages that allow for cooperative multitasking and efficient asynchronous programming. C++ introduced the concept of coroutines in the C++20 standard, providing a new way to write concurrent and asynchronous code. Coroutines allow functions to be suspended and resumed, offering greater control over program flow and resource management.

In this blog post, we will explore coroutine resumption strategies in C++, looking at different ways to resume and manage coroutines. We will discuss three common strategies: manual resumption, awaitable resumption, and custom resumption.

## 1. Manual Resumption

In the manual resumption strategy, coroutines are explicitly resumed by the caller using the `resume()` function. This approach gives the caller full control over when and how coroutines are resumed.

```cpp
#include <iostream>
#include <coroutine>

struct Task {
    struct promise_type {
        Task get_return_object() {
            return {};
        }
        std::suspend_never initial_suspend() {
            return {};
        }
        std::suspend_never final_suspend() noexcept {
            return {};
        }
        void return_void() {}
        void unhandled_exception() {}
    };

    std::coroutine_handle<promise_type> coro;

    explicit Task(std::coroutine_handle<promise_type> coro) : coro(coro) {}

    void resume() {
        coro.resume();
    }
};

Task myCoroutine() {
    std::cout << "Coroutine started\n";
    co_await std::suspend_always{};
    std::cout << "Coroutine resumed\n";

    co_return;
}

int main() {
    Task task = myCoroutine();
    task.resume();

    return 0;
}
```

In this example, the `myCoroutine()` function is defined as a coroutine using the `co_await` keyword. The `Task` struct is used to wrap the coroutine handle and provides a `resume()` function to explicitly resume the coroutine. In the `main()` function, we create an instance of `Task` and manually resume the coroutine.

## 2. Awaitable Resumption

The awaitable resumption strategy leverages the `co_await` mechanism to automatically resume coroutines when the awaited tasks are completed. This approach allows for more elegant and readable code by removing the need for explicit resumption.

```cpp
#include <iostream>
#include <coroutine>

struct Task {
    struct promise_type {
        Task get_return_object() {
            return {};
        }
        std::suspend_never initial_suspend() {
            return {};
        }
        std::suspend_never final_suspend() noexcept {
            return {};
        }
        void return_void() {}
        void unhandled_exception() {}
    };

    std::coroutine_handle<promise_type> coro;

    explicit Task(std::coroutine_handle<promise_type> coro) : coro(coro) {}

    bool await_ready() const noexcept {
        return !coro || coro.done();
    }

    void await_suspend(std::coroutine_handle<>) const noexcept {}

    void await_resume() const noexcept {
        coro.resume();
    }
};

Task myCoroutine() {
    std::cout << "Coroutine started\n";
    co_await std::suspend_always{};
    std::cout << "Coroutine resumed\n";

    co_return;
}

int main() {
    Task task = myCoroutine();
    task.await_resume();
    
    return 0;
}
```

In this example, the `Task` struct implements the `await_suspend()` and `await_resume()` functions. The `await_ready()` function is also implemented to check if the coroutine is already completed. By using the `co_await` keyword to await the completion of the coroutine, the resumption is handled automatically.

## 3. Custom Resumption

In some cases, you may need to implement a custom resumption strategy based on specific requirements. This can be useful if you want to control the logic and conditions for resuming coroutines.

```cpp
#include <iostream>
#include <coroutine>

struct Task {
    struct promise_type {
        Task get_return_object() {
            return {};
        }
        std::suspend_always initial_suspend() {
            return {};
        }
        std::suspend_always final_suspend() noexcept {
            return {};
        }
        void return_void() {}
        void unhandled_exception() {}
    };

    std::coroutine_handle<promise_type> coro;

    explicit Task(std::coroutine_handle<promise_type> coro) : coro(coro) {}

    void custom_resume() {
        if (!coro.done()) {
            coro.resume();
        }
    }
};

Task myCoroutine() {
    std::cout << "Coroutine started\n";
    
    // Custom condition for resuming the coroutine
    if (some_condition) {
        co_await std::suspend_always{};
    }
    
    std::cout << "Coroutine resumed\n";

    co_return;
}

int main() {
    Task task = myCoroutine();
    task.custom_resume();
    
    return 0;
}
```

In this example, the `Task` struct provides a `custom_resume()` function that implements a custom condition for resuming the coroutine. The coroutine is only resumed if a specific condition (`some_condition`) is met. This allows for more fine-grained control over the resumption of coroutines as per the application's requirements.

## Conclusion

Coroutine resumption strategies in C++ offer different ways to control and manage the execution of coroutines. Whether it is manual resumption, awaitable resumption, or custom resumption, each strategy has its advantages and use cases. By understanding these strategies, developers can effectively leverage coroutines to write efficient and scalable asynchronous code.

#programming #coroutines