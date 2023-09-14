---
layout: post
title: "Implementing functors with default arguments in C++"
description: " "
date: 2023-09-14
tags: [cplusplus, functors]
comments: true
share: true
---

In C++, functors offer a powerful way to create objects that can be called like functions. They are often used in scenarios that require custom sorting, filtering, or transformations. Functors can also accept arguments, making them even more versatile. In this article, we will explore how to implement functors with default arguments, which allow us to provide fallback values if certain arguments are not passed.

## What are Functors?

Functors, also known as function objects, are objects that can be used as if they were regular functions. They achieve this by overloading the function call operator `()`. This allows instances of a functor class to be invoked just like a function call.

## Implementation

To implement functors with default arguments, we can utilize the power of C++ constructor overloading. Let's illustrate this with an example of a simple addition functor that takes two arguments, `a` and `b`, with `b` having a default value of 0.

```cpp
class AddFunctor {
public:
  AddFunctor(int a, int b = 0)
    : a_(a), b_(b) {}

  int operator()() const {
    return a_ + b_;
  }

private:
  int a_;
  int b_;
};
```

In the above code, we define the `AddFunctor` class that takes two arguments, `a` and `b`, in its constructor. The `b` argument has a default value of 0. The overloaded `operator()` function performs the addition operation and returns the result.

## Usage

Let's now see how we can use the `AddFunctor` with and without providing the default argument.

```cpp
int main() {
  AddFunctor add1(5);
  cout << "Addition without default argument: " << add1() << endl;  // Output: 5

  AddFunctor add2(5, 3);
  cout << "Addition with default argument: " << add2() << endl;  // Output: 8

  return 0;
}
```

In the code above, we create two instances of the `AddFunctor`. The first instance, `add1`, only provides the required argument `a`, and the default value of `b` is used. The second instance, `add2`, provides both `a` and `b` arguments explicitly. When we invoke the functors using the `()` operator, we get the correct addition operation result.

## Conclusion

Functors are a powerful feature in C++ that enables objects to behave like functions. By implementing functors with default arguments, we can provide fallback values and make our programs more flexible. This allows us to create reusable and customizable code, enhancing the overall efficiency and readability of our C++ programs.

#cplusplus #functors #C++