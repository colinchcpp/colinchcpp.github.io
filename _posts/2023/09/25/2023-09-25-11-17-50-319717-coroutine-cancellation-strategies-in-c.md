---
layout: post
title: "Coroutine cancellation strategies in C++"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

Coroutines are powerful programming constructs that allow you to write asynchronous code in a sequential, easier-to-understand manner. However, one challenge with coroutines is managing their cancellation in a controlled manner. In this blog post, we will explore various strategies for canceling coroutines in C++.

## 1. Cooperative Cancellation

Cooperative cancellation relies on the coroutine itself to periodically check for a cancellation flag and gracefully exit. This approach ensures that the coroutine gracefully terminates when requested.

```cpp
#include <iostream>
#include <experimental/coroutine>

class cancellable_task {
public:
  struct promise_type {
    bool cancelled = false;
    auto get_return_object() { return cancellable_task{this}; }
    auto initial_suspend() { return std::experimental::suspend_never{}; }
    auto final_suspend() noexcept { return std::experimental::suspend_always{}; }
    void unhandled_exception() { std::terminate(); }
    void return_void() {}
    void cancel() { cancelled = true; }
  };

  cancellable_task(promise_type* p) : promise_(p) {}
  
  bool await_ready() const noexcept { return promise_->cancelled; }
  void await_suspend(std::experimental::coroutine_handle<>) const noexcept {}
  void await_resume() const noexcept {}
private:
  promise_type* promise_;
};

cancellable_task my_coroutine() {
  std::cout << "Coroutine started\n";
  co_await cancellable_task{};
  std::cout << "Coroutine resumed\n";
}

int main() {
  auto coroutine = my_coroutine();
  
  // Cancelling the coroutine
  coroutine.promise().cancel();
  
  // Resuming the coroutine
  coroutine.resume();
  
  return 0;
}
```

In the example above, we define a `cancellable_task` that uses a `promise_type` containing a `cancelled` flag. Using this flag, the coroutine checks for cancellation and gracefully terminates if requested.

## 2. Time-based Cancellation

Another strategy for coroutine cancellation is time-based cancellation. This approach cancels the coroutine if it exceeds a specified time limit. This can be useful in scenarios where you want to limit the execution time of a coroutine.

```cpp
#include <iostream>
#include <experimental/coroutine>
#include <chrono>

class timed_task {
public:
  struct promise_type {
    std::chrono::steady_clock::time_point deadline;
    
    auto get_return_object() { return timed_task{this}; }
    auto initial_suspend() { return std::experimental::suspend_never{}; }
    auto final_suspend() noexcept { return std::experimental::suspend_always{}; }
    void unhandled_exception() { std::terminate(); }
    void return_void() {}
    void set_deadline(const std::chrono::steady_clock::time_point& t) { deadline = t; }
  };

  timed_task(promise_type* p) : promise_(p) {}

  bool await_ready() const noexcept { return std::chrono::steady_clock::now() >= promise_->deadline; }
  void await_suspend(std::experimental::coroutine_handle<>) const noexcept {}
  void await_resume() const noexcept {}
private:
  promise_type* promise_;
};

timed_task my_coroutine() {
  std::cout << "Coroutine started\n";
  co_await timed_task{std::chrono::steady_clock::now() + std::chrono::seconds{5}};
  std::cout << "Coroutine resumed\n";
}

int main() {
  auto coroutine = my_coroutine();
  
  // Resuming the coroutine
  coroutine.resume();
  
  return 0;
}
```

In this example, the `timed_task` coroutine awaits for a specified time duration and cancels itself if the deadline is reached.

## Conclusion

Managing coroutine cancellation is essential to prevent resource leaks and ensure the efficient utilization of system resources. By using cooperative or time-based cancellation strategies, you can gracefully cancel and manage your coroutines in C++. Always consider the specific requirements of your application and choose the appropriate cancellation strategy accordingly.

**#Coroutines #Cancellation #C++**

Note: The code examples provided in this blog post are based on experimental C++20 features and may require compiler-specific flags or features.