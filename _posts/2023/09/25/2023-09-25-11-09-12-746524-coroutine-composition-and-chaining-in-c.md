---
layout: post
title: "Coroutine composition and chaining in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Coroutines in C++ are a powerful tool for writing asynchronous code in a sequential and easy-to-read manner. They allow developers to write code that looks and behaves like synchronous code, while still reaping the benefits of asynchronous execution. One key feature of coroutines is their ability to be composed and chained together to create more complex and flexible asynchronous workflows.

## Composition using `co_await`

In C++, coroutines can be composed using the `co_await` operator. This operator allows a coroutine to suspend its execution and wait for the completion of another coroutine. By using `co_await`, you can build a pipeline of coroutines, where the output of one coroutine becomes the input of the next, forming a chain of asynchronous operations.

Here's an example of coroutine composition in C++:

```cpp
#include <iostream>
#include <experimental/coroutine>

// Coroutine 1: Adds 1 to the input value
int coroutine1(int value) {
    co_return value + 1;
}

// Coroutine 2: Multiplies the input value by 2
int coroutine2(int value) {
    co_return value * 2;
}

// Coroutine composition
int composedCoroutine(int value) {
    int result = co_await coroutine1(value);
    result = co_await coroutine2(result);
    co_return result;
}

int main() {
    int value = 5;
    int result = composedCoroutine(value);
    std::cout << "Result: " << result << std::endl;  // Output: Result: 12
    return 0;
}
```

In this example, `composedCoroutine` is a coroutine that sequentially chains `coroutine1` and `coroutine2` together. The result of `coroutine1` becomes the input to `coroutine2`, and the final result is returned.

## Chaining using Coroutine Types

Another way to achieve coroutine chaining in C++ is by using coroutine types. By defining a coroutine type that represents a series of asynchronous operations, you can easily chain coroutines together using standard control flow constructs such as `if` statements, loops, or function calls.

Here's an example of coroutine chaining using coroutine types in C++:

```cpp
#include <iostream>
#include <experimental/coroutine>

// Coroutine 1: Adds 1 to the input value
int coroutine1(int value) {
    co_return value + 1;
}

// Coroutine 2: Multiplies the input value by 2
int coroutine2(int value) {
    co_return value * 2;
}

// Coroutine type representing a chain of coroutines
struct CoroutineChain {
    int value;

    // Coroutine 1
    int coroutine1() {
        value = co_await ::coroutine1(value);
    }

    // Coroutine 2
    int coroutine2() {
        value = co_await ::coroutine2(value);
    }

    // Entry point coroutine
    int start() {
        co_await coroutine1();
        co_await coroutine2();
        co_return value;
    }
};

int main() {
    int value = 5;
    CoroutineChain chain{value};
    int result = chain.start();
    std::cout << "Result: " << result << std::endl;  // Output: Result: 12
    return 0;
}
```

In this example, `CoroutineChain` defines a series of coroutines (`coroutine1` and `coroutine2`), each responsible for a specific asynchronous operation. The `start` coroutine acts as the entry point, sequentially chaining the other coroutines together. The result is returned at the end of the chain.

## Conclusion

Coroutines in C++ provide a powerful mechanism for composing and chaining together asynchronous operations in a sequential and readable manner. Whether using the `co_await` operator or coroutine types, developers can easily build complex asynchronous workflows by combining and reusing smaller coroutines. This flexibility and composability make coroutines an essential tool for writing asynchronous code in C++.

#C++ #Coroutines