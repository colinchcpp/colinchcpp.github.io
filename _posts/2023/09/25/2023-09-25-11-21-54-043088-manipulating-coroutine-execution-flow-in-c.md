---
layout: post
title: "Manipulating coroutine execution flow in C++"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

Coroutines are a powerful tool in modern C++ that allow for easy handling of asynchronous code. They enable developers to write code that looks synchronous, while still providing the benefits of asynchronous execution. In this article, we will explore how to manipulate the execution flow of coroutines in C++.

## Suspending and resuming coroutines ##

Coroutines in C++ can be suspended and resumed using the `co_yield` statement. This allows the coroutine to pause its execution and return control back to the caller. When resumed, the execution continues from the point of suspension. This mechanism enables the manipulation of execution flow within coroutines.

**Example:**

```
#include <iostream>
#include <experimental/coroutine>

class MyCoroutine {
public:
  struct promise_type {
    MyCoroutine get_return_object() {
      return MyCoroutine{
        std::experimental::coroutine_handle<promise_type>::from_promise(*this)
      };
    }

    std::experimental::suspend_never initial_suspend() noexcept { return {}; }
    std::experimental::suspend_always final_suspend() noexcept { return {}; }
    void return_void() noexcept {}
    void unhandled_exception() noexcept {}
  };

  MyCoroutine(std::experimental::coroutine_handle<promise_type> handle)
    : handle(handle) {}

  ~MyCoroutine() {
    if (handle) handle.destroy();
  }

  bool move_next() {
    if (!handle.done()) {
      handle.resume();
    }
    return !handle.done();
  }

private:
  std::experimental::coroutine_handle<promise_type> handle;
};

MyCoroutine doSomeWork() {
  std::cout << "Starting coroutine..." << std::endl;

  co_yield; // Suspend coroutine execution

  std::cout << "Resumed coroutine..." << std::endl;
}

int main() {
  MyCoroutine coroutine = doSomeWork();
  
  std::cout << "Starting main..." << std::endl;
  
  while (coroutine.move_next()) {
    // Coroutine is not finished
  }
  
  std::cout << "Finished main." << std::endl;
  
  return 0;
}
```

In the example above, we create a coroutine `doSomeWork()` that prints a message, suspends its execution using `co_yield`, and then prints a second message when resumed. Inside `main()`, we create an instance of `MyCoroutine` and repeatedly call `move_next()` until the coroutine is done.

## Controlling coroutine execution flow ##

To control the execution flow of coroutines, we can use conditions and loops inside the coroutine body. By defining conditional statements with `if` and `switch`, we can decide whether or not to suspend the coroutine or make it jump to a different point of execution.

**Example:**

```cpp
MyCoroutine doWorkWithCondition() {
  std::cout << "Starting coroutine with condition..." << std::endl;

  bool shouldSuspend = true;

  if (shouldSuspend) {
    std::cout << "Suspending coroutine..." << std::endl;
    co_yield;  // Suspend coroutine execution
  }

  std::cout << "Resumed coroutine..." << std::endl;

  int iterations = 3;
  for (int i = 0; i < iterations; ++i) {
    std::cout << "Iteration " << i << std::endl;
    co_yield; // Suspend coroutine execution
  }

  std::cout << "Finished coroutine." << std::endl;
}
```

In the above example, we introduce a condition `shouldSuspend` that determines whether the coroutine suspends or proceeds with execution. We also use a `for` loop to loop a specific number of iterations and suspend the coroutine each time.

By controlling the execution flow of coroutines using conditions, loops, and the suspension mechanism provided by `co_yield`, we can build powerful and flexible asynchronous code in C++.

#coroutines #C++