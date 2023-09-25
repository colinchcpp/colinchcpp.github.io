---
layout: post
title: "Passing arguments to coroutines in C++"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Coroutines in C++ are powerful tools for writing asynchronous code that is easy to read and maintain. They allow you to write code that looks like synchronous code but behaves asynchronously. One common question that arises when working with coroutines is how to pass arguments to them.

## 1. Using Function Parameters

The most straightforward way to pass arguments to a coroutine is to use function parameters. In C++, you can define your coroutine function to accept parameters just like any other function:

```cpp
#include <iostream>
#include <experimental/coroutine>

using namespace std;

generator<int> count_up_to(int limit) {
    for (int i = 1; i <= limit; ++i) {
        co_yield i;
    }
}

int main() {
    for (auto num : count_up_to(5)) {
        cout << num << ' ';
    }

    return 0;
}
```

In the example above, the `count_up_to` coroutine takes an `int` parameter `limit` and yields numbers from 1 to the given limit. When calling the coroutine using the range-based for loop, you can pass the desired limit as an argument.

## 2. Using Member Variables

Another way to pass data to coroutines is by using member variables. You can define a class that encapsulates the coroutine and pass arguments to it by setting the corresponding member variables:

```cpp
#include <iostream>
#include <experimental/coroutine>

using namespace std;

class Counter {
public:
    Counter(int limit) : limit_(limit) {}

    generator<int> count_up() {
        for (int i = 1; i <= limit_; ++i) {
            co_yield i;
        }
    }

private:
    int limit_;
};

int main() {
    Counter counter(5);

    for (auto num : counter.count_up()) {
        cout << num << ' ';
    }

    return 0;
}
```

In this example, the `Counter` class is used to encapsulate the coroutine logic. The constructor takes the desired limit as an argument and assigns it to the `limit_` member variable. The `count_up` member function is responsible for generating the sequence of numbers.

## Conclusion

Passing arguments to coroutines in C++ can be done using function parameters or member variables. This allows you to customize the behavior of the coroutine to fit your specific needs. Experiment with these techniques and enjoy the benefits of writing asynchronous code with coroutines.

#cpp #coroutines