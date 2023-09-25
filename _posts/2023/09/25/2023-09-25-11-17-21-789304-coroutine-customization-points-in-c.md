---
layout: post
title: "Coroutine customization points in C++"
description: " "
date: 2023-09-25
tags: [Coroutines]
comments: true
share: true
---
Coroutines are a powerful feature introduced in C++20 that allow you to write asynchronous code in a sequential and structured manner. They provide a way to suspend and resume the execution of a function, making it easier to handle asynchronous operations.

C++20 introduces a set of customization points that allow you to customize the behavior of coroutines. These customization points are special functions that can be defined by the programmer to modify the default behavior of coroutines.

## 1. `promise_type`
The `promise_type` is responsible for managing the coroutine state and handling the result of a coroutine. By defining a custom `promise_type`, you can customize the way a coroutine behaves and handles its result.

To define a custom `promise_type`, you need to define a struct that meets the PromiseType requirements. These requirements include defining member functions like `get_return_object`, `initial_suspend`, `final_suspend`, and `return_void`.

Here's an example of a custom `promise_type` for a simple coroutine that returns a value:
```cpp
struct custom_promise {
    int value;

    int get_return_object() {
        return value;
    }

    std::suspend_never initial_suspend() noexcept { return {}; }
    std::suspend_never final_suspend() noexcept { return {}; }
    void return_value(int val) { value = val; }
};
```

## 2. `initial_suspend` and `final_suspend`
The `initial_suspend` and `final_suspend` customization points allow you to define the initial and final suspends of a coroutine.

The `initial_suspend` customization point determines what happens when a coroutine is first started. By default, coroutines are asynchronously started, meaning they are immediately suspended after being called. If you need to change this behavior, you can define a custom `initial_suspend` function.

The `final_suspend` customization point defines what happens after the coroutine has completed its execution. By default, coroutines are not resumed after completion. Again, if you need different behavior, you can define a custom `final_suspend` function.

Here's an example of customizing the `initial_suspend` and `final_suspend` points:
```cpp
struct custom_promise {
    std::suspend_always initial_suspend() noexcept { return {}; }
    std::suspend_always final_suspend() noexcept { return {}; }
};
```

## Conclusion
Customization points in coroutines provide a way to tailor the behavior of coroutines to your specific needs. By defining a custom `promise_type`, you can control how coroutines handle their result. The `initial_suspend` and `final_suspend` customization points allow you to modify the suspending behavior at the start and end of a coroutine's execution.

With these customization points, you have more control over the execution flow of your coroutines, making them even more powerful and flexible. So go ahead and explore the possibilities of customizing coroutines in C++. #C++ #Coroutines