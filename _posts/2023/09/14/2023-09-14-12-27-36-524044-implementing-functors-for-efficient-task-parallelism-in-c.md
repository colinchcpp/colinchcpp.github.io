---
layout: post
title: "Implementing functors for efficient task parallelism in C++"
description: " "
date: 2023-09-14
tags: []
comments: true
share: true
---

When it comes to writing efficient parallel code in C++, functors can be a powerful tool. Functors are objects that can be used as function pointers, allowing for more flexibility and control in how tasks are executed. In this article, we will explore how to implement functors for efficient task parallelism in C++.

## What is Task Parallelism?

Task parallelism is a programming paradigm that involves dividing large tasks into smaller, independent subtasks that can be executed concurrently. This is particularly useful when dealing with computationally intensive tasks or when maximizing the utilization of multi-core processors.

## Implementing Functors

A functor in C++ is an object that can be invoked as if it were a function. They are typically implemented as classes or structures that overload the `operator()` function. By making use of functors, we can encapsulate the logic of individual tasks and easily distribute them across multiple threads for parallel execution.

Here is an example implementation of a functor that squares a given number:

```cpp
class SquareFunctor {
public:
    int operator()(int num) const {
        return num * num;
    }
};
```

To use our functor, we can create an instance of it and invoke it like a regular function:

```cpp
SquareFunctor square;
int result = square(5);
```

## Utilizing Functors for Task Parallelism

To leverage functors for task parallelism, we can use the `std::async` function from the C++ standard library. This function schedules the execution of a given task asynchronously and returns a `std::future` object representing the result of the computation.

Here's an example of a functor that performs a computationally intensive task, such as calculating the factorial of a number:

```cpp
class FactorialFunctor {
public:
    unsigned long long operator()(unsigned int num) const {
        unsigned long long result = 1;
        for (unsigned int i = 1; i <= num; ++i) {
            result *= i;
        }
        return result;
    }
};
```

To parallelize the calculation of factorials using multiple threads, we can use `std::async` as follows:

```cpp
FactorialFunctor factorial;

// Schedule multiple factorial computations in parallel
std::future<unsigned long long> futureResult1 = std::async(factorial, 5);
std::future<unsigned long long> futureResult2 = std::async(factorial, 10);

// Wait for the results and retrieve them
unsigned long long result1 = futureResult1.get();
unsigned long long result2 = futureResult2.get();
```

By using functors in conjunction with `std::async`, we can easily distribute independent tasks across multiple threads. This allows for efficient utilization of available hardware resources and can greatly improve the overall performance of our applications.

## Conclusion

Functors provide a powerful mechanism to encapsulate the logic of individual tasks and enable efficient task parallelism in C++. By leveraging functors with the `std::async` function, we can easily distribute computations across multiple threads, thus maximizing the utilization of multi-core processors.