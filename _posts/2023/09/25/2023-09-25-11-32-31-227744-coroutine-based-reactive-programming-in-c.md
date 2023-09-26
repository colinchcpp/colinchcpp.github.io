---
layout: post
title: "Coroutine-based reactive programming in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

In recent years, reactive programming has gained popularity due to its ability to handle asynchronous and event-driven programming models. One approach to achieve reactive programming in C++ is by using coroutines, which were introduced in C++20 and provide a powerful way to write asynchronous code in a sequential manner. In this article, we will explore coroutine-based reactive programming in C++ and the benefits it brings.

## What are coroutines?

Coroutines are a special kind of function that can be suspended and resumed during execution. They allow you to write asynchronous code in a more synchronous and straightforward manner. When a coroutine encounters a suspension point, it yields control back to the caller, allowing other code to execute. Once the suspended code is ready to continue, it can be resumed, picking up where it left off.

## Reactive programming with coroutines

By combining coroutines with reactive programming, we can create a powerful mechanism to handle asynchronous and event-driven flows. Reactive programming is based on the concept of streams, which represent a sequence of events or values over time. With coroutines, we can treat streams as input sources and use asynchronous operations to act upon them.

To implement reactive programming with coroutines, we need a library that provides support for reactive streams and coroutines. One popular library is **cppcoro**[^1^], which offers a range of utilities for working with coroutines in C++. It includes support for asynchronous operations, cancellation, and timer-based scheduling.

## Example: Reactive stream using coroutines

Let's take a look at an example of how we can create a reactive stream using coroutines.

```cpp
#include <cppcoro/async_generator.hpp>
#include <cppcoro/task.hpp>

cppcoro::async_generator<int> createReactiveStream()
{
    for (int i = 0; i < 10; ++i)
    {
        // Simulate asynchronous operation
        co_await cppcoro::task_resumed_on{co_await cppcoro::task_delay(std::chrono::seconds(1))};

        co_yield i;
    }
}

cppcoro::task<void> consumeReactiveStream()
{
    auto stream = createReactiveStream();

    async for (const auto& value : stream)
    {
        // Process received value
        std::cout << "Received value: " << value << std::endl;
    }
}

int main()
{
    consumeReactiveStream().resume_on(std::this_thread::get_executor()).block();
    return 0;
}
```

In this example, we define a coroutine `createReactiveStream()` that generates a stream of integers asynchronously. On each iteration, we simulate an asynchronous operation using `cppcoro::task_delay()` and `cppcoro::task_resumed_on`. We then use `co_yield` to emit the next value in the stream.

To consume the reactive stream, we define another coroutine `consumeReactiveStream()` that awaits values from the stream using the `async for` loop introduced in C++20. Each received value is processed accordingly.

Finally, in the `main()` function, we invoke `consumeReactiveStream()` and block until the stream is consumed.

## Conclusion

By harnessing the power of coroutines, we can achieve a more concise and readable way to implement reactive programming in C++. The combination of coroutines and reactive streams enables us to handle complex asynchronous flows with ease. With libraries like **cppcoro**, we have powerful tools at our disposal to write efficient, maintainable, and scalable reactive code.

_#cplusplus #reactiveprogramming_

[^1^]: [cppcoro - GitHub](https://github.com/lewissbaker/cppcoro)