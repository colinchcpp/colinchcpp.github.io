---
layout: post
title: "C++20 enhancements to coroutines"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

Coroutines are a popular feature in modern programming languages that allow developers to write asynchronous code in a more structured and readable manner. In C++20, coroutines have received some significant enhancements, making them even more powerful and versatile. In this article, we'll explore some of the key improvements introduced in C++20 for coroutines.

## 1. `co_await` and `co_yield`

C++20 introduces the keywords `co_await` and `co_yield` to simplify coroutine operations. The `co_await` keyword is used to suspend the execution of a coroutine until the awaited task is completed. It allows you to write asynchronous code in a more sequential style, making it easier to understand and maintain.

```cpp
#include <iostream>
#include <experimental/coroutine>

std::experimental::suspend_always operator co_await (std::experimental::suspend_always awaitable) noexcept {
    // suspend the coroutine until awaitable is complete
    co_yield awaitable;
}

std::experimental::suspend_never operator co_await (std::experimental::suspend_never awaitable) noexcept {
    // resume the coroutine immediately
    co_return;
}

int main() {
    std::experimental::suspend_always awaitable{};

    std::cout << "Before co_await\n";

    co_await awaitable;

    std::cout << "After co_await\n";
}
```

In the example above, the `operator co_await` is overloaded to handle `suspend_always` and `suspend_never` types. When `co_await` is called with `suspend_always`, the coroutine suspends until the awaitable is complete. On the other hand, when `co_await` is called with `suspend_never`, the coroutine resumes execution immediately.

## 2. `co_return` with values

In C++20, coroutines can now use `co_return` to return values from a coroutine. This simplifies the previous requirement of using `co_await` with a promise to retrieve the final result.

```cpp
#include <iostream>
#include <experimental/coroutine>

std::experimental::suspend_always operator co_await (std::experimental::suspend_always awaitable) noexcept {
    // suspend the coroutine until awaitable is complete
    co_yield awaitable;
}

std::experimental::suspend_never operator co_await (std::experimental::suspend_never awaitable) noexcept {
    // resume the coroutine immediately
    co_return;
}

std::experimental::suspend_always task1() {
    co_return 42;
}

std::experimental::suspend_always task2() {
    co_return 100;
}

std::experimental::suspend_always multipleTasks() {
    int result1 = co_await task1();
    int result2 = co_await task2();

    std::cout << "Result: " << result1 + result2 << '\n';
}

int main() {
    multipleTasks();
}
```

In the above example, the `multipleTasks()` coroutine uses `co_return` to return the final result. It awaits two different tasks `task1()` and `task2()`, and then calculates and prints the sum of the results. This improves code readability by eliminating the need for separate promise objects and additional boilerplate code.

## Conclusion

C++20 brings powerful enhancements to coroutines, making asynchronous programming in C++ simpler and more readable. The introduction of `co_await`, `co_yield`, and `co_return` keywords provides a more intuitive way to work with coroutines and allows for better control over asynchronous code flow. These improvements make C++ coroutines even more appealing for developing efficient and elegant asynchronous applications.

`#cpp` `#coroutines`