---
layout: post
title: "Handling exceptions in C++ coroutines"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

C++20 introduced coroutines, a powerful feature that allows developers to write asynchronous code in a more sequential and readable manner. However, working with coroutines also introduces the need to handle exceptions properly. In this blog post, we will explore the various techniques for handling exceptions in C++ coroutines.

## 1. `co_await` inside try-catch block

When using `co_await` inside a coroutine, it is best to wrap the `co_await` expression inside a try-catch block to handle any exceptions that might be thrown. This ensures that exceptions are caught within the coroutine itself, allowing for proper error handling and recovery.

```cpp
#include <exception>
#include <iostream>
#include <experimental/coroutine>

using namespace std;
using namespace std::experimental;

struct custom_exception : public exception {};

generator<int> coroutine_func() {
    try {
        co_await some_awaitable_expression();
        co_yield 42;
    } catch (const custom_exception& ex) {
        cerr << "Caught custom_exception: " << ex.what() << endl;
        // handle exception
    }
    // other code
}
```

## 2. Propagating exceptions from coroutines

Sometimes, you may want to propagate exceptions from a coroutine to the caller. To achieve this, you can use the `co_yield` statement to rethrow the exception, allowing the caller to handle it accordingly.

```cpp
generator<int> coroutine_func() {
    try {
        co_await some_awaitable_expression();
        co_yield 42;
    } catch (const custom_exception& ex) {
        co_yield -1;  // rethrow exception
    }
    // other code
}
```

When calling the coroutine, the caller can use a `try-catch` block to handle the exception that is propagated:

```cpp
try {
    generator<int> gen = coroutine_func();
    for (int val : gen) {
        // process values
    }
} catch (const custom_exception& ex) {
    cerr << "Caught custom_exception: " << ex.what() << endl;
    // handle exception
}
```

## Conclusion

Handling exceptions in C++ coroutines is an essential aspect of writing robust and error-tolerant asynchronous code. By using try-catch blocks inside coroutines and propagating exceptions to the caller, you can implement proper error handling and recovery mechanisms. Remember to always consider potential exception scenarios when working with coroutines to ensure reliable and stable code.

#C++ #coroutines