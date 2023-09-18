---
layout: post
title: "Implementing functors for currying and partial application in C++"
description: " "
date: 2023-09-14
tags: [CurryingInC, PartialApplicationInC]
comments: true
share: true
---

Currying and partial application are powerful techniques in functional programming that allow us to create new functions by partially applying arguments to existing functions. In C++, we can implement functors to achieve currying and partial application. In this blog post, we will explore how to implement functors in C++ to enable these functional programming techniques.

## What is a Functor?

In C++, a functor is an object that can be treated as if it were a function. Functors are useful because they can have state and can be customized based on the required functionality.

## Currying

Currying is a technique where a function that takes multiple arguments is transformed into a sequence of functions, each taking a single argument. This allows us to partially apply arguments to a function, creating new functions with fewer parameters.

To implement currying using functors in C++, we can define a class that overloads the `operator()` with multiple versions, each taking a single argument. Here's an example implementation:

```cpp
class Curry {
public:
    Curry(int x) : x(x) {}

    int operator()(int y) {
        return x + y;
    }

private:
    int x;
};

int main() {
    Curry add5(5);
    int result = add5(3); // Partial application
    // result = 8

    return 0;
}
```

Here, the `Curry` class takes an integer `x` in its constructor and overloads the `operator()` to take a single argument. We can create an instance of `Curry` with an initial value `5` and then partially apply it with another value `3`, resulting in `8`.

## Partial Application

Partial application is similar to currying but allows us to fix some, but not all, arguments of a function. This technique creates a new function with the remaining arguments that can be called later.

To implement partial application using functors in C++, we can use a similar approach as currying but allow the function to accept different types and arguments. Here's an example implementation:

```cpp
#include <iostream>

class Adder {
public:
    Adder() : sum(0) {}

    void operator()(int value) {
        sum += value;
    }

    template<typename... Args>
    void operator()(int value, Args... args) {
        sum += value;
        (*this)(args...);
    }

    int getResult() {
        return sum;
    }

private:
    int sum;
};

int main() {
    Adder adder;
    adder(1);
    adder(2);
    adder(3, 4, 5);
    int result = adder.getResult();
    // result = 15

    return 0;
}
```

In this example, the `Adder` class acts as a functor that can accept multiple arguments of different types. The `operator()` overload takes an integer value and updates the `sum` member variable. Additionally, we define a variadic template `operator()` to accept any number of arguments and recursively call itself until all arguments are processed.

With this implementation, we can partially apply arguments to the `Adder` functor, accumulating the sum of all the values passed. In the example above, we call `adder` multiple times with different sets of arguments and finally retrieve the accumulated sum.

## Conclusion

By implementing functors in C++, we can enable currying and partial application, two powerful techniques in functional programming. Functors allow us to create reusable and customizable objects that act like functions, providing flexibility and utility. Incorporating these techniques in our code can result in cleaner, more concise, and more flexible codebases.

#CurryingInC++ #PartialApplicationInC++