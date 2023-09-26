---
layout: post
title: "Coroutine timeouts and cancellation tokens in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

In modern C++, coroutines have become a powerful tool for writing asynchronous code that is both efficient and readable. With the introduction of the C++20 standard, coroutines have gained even more functionality, including the ability to handle timeouts and cancellation.

## Timeouts in Coroutines

One common use case when dealing with asynchronous operations is setting a timeout to limit the amount of time a coroutine will wait for a certain operation to complete. This is particularly useful when dealing with network requests, where a coroutine should not wait indefinitely for a response.

To implement timeouts in coroutines, we can use the `<chrono>` library to measure time durations. Here's an example:

```cpp
#include <iostream>
#include <chrono>
#include <experimental/coroutine>

using namespace std::chrono_literals;

std::experimental::coroutine_handle<> current_coroutine;

template<typename Rep, typename Period>
std::experimental::suspend_always timeout(std::chrono::duration<Rep, Period> duration)
{
    auto start_time = std::chrono::steady_clock::now();
    while (std::chrono::steady_clock::now() - start_time < duration)
    {
        co_await std::experimental::suspend_never{};
    }
    current_coroutine.destroy();
}

template<typename Func, typename... Args>
void run_with_timeout(std::chrono::duration<long long, std::milli> duration, Func&& func, Args&&... args)
{
    current_coroutine = std::experimental::coroutine_handle<>::from_address(nullptr);
    timeout(duration);
    func(std::forward<Args>(args)...);
}

int main()
{
    run_with_timeout(200ms, [](){
        std::cout << "Executing in limited time\n";
    });
    return 0;
}
```

In this example, we define a `timeout` coroutine that simply suspends the execution until the specified duration has passed. If the coroutine is not resumed within the given timeout, `current_coroutine.destroy()` is called to cancel execution.

We also define a helper function `run_with_timeout` that takes a timeout duration and a function to execute. Inside `run_with_timeout`, we first initialize our `current_coroutine` handle to be able to destroy it later if needed. Then, we call `timeout` coroutine and pass the specified duration. Finally, we execute the provided function.

In our `main` function, we invoke `run_with_timeout` with a timeout of 200 milliseconds and a lambda that prints a message. If the lambda doesn't finish execution within the given timeout, it will be canceled.

## Cancellation Tokens in Coroutines

Another important feature when dealing with asynchronous code is the ability to cancel ongoing operations. Cancellation tokens allow us to propagate a cancellation request throughout a set of coroutines, terminating them early if needed.

Here's an example of using cancellation tokens in coroutines:

```cpp
#include <iostream>
#include <experimental/coroutine>

struct cancellation_token
{
    bool is_cancelled = false;
    
    bool is_cancellation_requested() const noexcept
    {
        return is_cancelled;
    }
    
    void cancel() noexcept
    {
        is_cancelled = true;
    }
};

cancellation_token global_token;

template<typename T>
struct task
{
    struct promise_type
    {
        T value;
        
        task<T> get_return_object() noexcept
        {
            return task<T>{std::experimental::coroutine_handle<promise_type>::from_promise(*this)};
        }
        
        std::experimental::suspend_always initial_suspend() noexcept { return {}; }
        std::experimental::suspend_always final_suspend() noexcept { return {}; }
        void return_value(T value) noexcept { this->value = value; }
        void unhandled_exception() noexcept {}
    };
    
    std::experimental::coroutine_handle<promise_type> handle;
    
    explicit task(std::experimental::coroutine_handle<promise_type> handle) noexcept
        : handle(handle) {}
    
    ~task() noexcept { handle.destroy(); }
    
    bool await_ready() noexcept { return false; }
    
    void await_suspend(std::experimental::coroutine_handle<> waiting_coroutine) noexcept
    {
        if (global_token.is_cancellation_requested())
        {
            waiting_coroutine.destroy();
        }
        else
        {
            global_token.on_cancel([this, waiting_coroutine]() mutable {
                handle.destroy();
                waiting_coroutine.destroy();
            });
            handle.resume();
        }
    }
    
    auto await_resume() noexcept { return handle.promise().value; }
};

task<int> perform_long_running_task()
{
    // Simulating a long-running operation
    co_await std::experimental::suspend_always{};
    co_return 42;
}

int main()
{
    global_token.cancel();
    
    task<int> t = perform_long_running_task();
    
    std::cout << "Result: " << t.await_resume() << "\n";
    
    return 0;
}
```

In this example, we define a `cancellation_token` struct that keeps track of whether cancellation has been requested. It has a `cancel` method to trigger cancellation.

Next, we define a `task` struct, which represents the coroutine itself. The `task` has a `promise_type` nested struct that is responsible for managing the coroutine state. Within `promise_type`, we define the necessary functions like `get_return_object`, `initial_suspend`, `final_suspend`, etc.

The important part is the `await_suspend` function, where we check if cancellation has been requested. If so, we destroy both the `handle` of the current coroutine and the `waiting_coroutine` that was waiting for its completion. Otherwise, we set up a callback on the cancellation token, so if cancellation is later requested, we destroy both coroutines.

Finally, in the `main` function, we cancel the global token. Then, we create a task that represents our long-running operation, and we await its completion. Since cancellation has been requested, the task will be destroyed before completion, and we will not see any output.

## Conclusion

With coroutines and the C++20 standard, handling timeouts and cancellation tokens in asynchronous code has become easier and more expressive. Timeouts ensure that coroutines do not wait indefinitely for operations to complete, while cancellation tokens allow the propagation of cancellation requests, terminating ongoing coroutines early. By utilizing these features, we can write more robust and efficient asynchronous code in C++.