---
layout: post
title: "How to create functors that maintain state in C++"
description: " "
date: 2023-09-14
tags: [Functors]
comments: true
share: true
---

Functors are objects that can be used as if they were functions. They are commonly used in C++ to encapsulate state and behavior together. In this tutorial, we will learn how to create functors that maintain state in C++.

## What is a Functor?

In C++, a functor is an object that can be treated as if it were a function. It overloads the `operator()` and can be invoked like a regular function. Functors can store state and modify it between invocations, making them useful for maintaining context or stateful behavior.

## Creating a Functor

To create a functor, we will define a class and overload the `operator()` inside it. Let's start with a simple example of a counter functor that increments a counter each time it's called:

```cpp
class Counter {
public:
    Counter() : count(0) {}

    void operator()() {
        count++;
        std::cout << "Count: " << count << std::endl;
    }

private:
    int count;
};
```

In the above code, we define a `Counter` class that has an integer member variable `count`. The default constructor initializes `count` to 0. The `operator()` function increments `count` and prints its value.

## Using the Functor

Once we have defined the functor, we can use it just like a regular function. Here's how we can use the `Counter` functor:

```cpp
int main() {
    Counter counter;

    counter(); // Count: 1
    counter(); // Count: 2
    counter(); // Count: 3

    return 0;
}
```

In the `main()` function, we create an instance of the `Counter` functor called `counter`. We can invoke the `counter` object just like a function using the `()` operator. Each time we call it, the `count` variable is incremented and its value is printed.

## Conclusion

In this tutorial, we learned how to create functors that maintain state in C++. Functors are powerful constructs that allow us to encapsulate state and behavior together, providing a convenient way to write reusable and stateful code. By overloading the `operator()` inside a class, we can define our own functors and utilize them in our programs.

#C++ #Functors