---
layout: post
title: "C++ functors: combining object-oriented and functional programming paradigms"
description: " "
date: 2023-09-14
tags: [functors]
comments: true
share: true
---

In the world of programming, different paradigms offer different approaches to solving problems and organizing code. Two popular paradigms are **object-oriented programming** (OOP) and **functional programming** (FP). These paradigms have their own unique features and strengths, but sometimes it can be beneficial to combine elements of both paradigms to create more flexible and powerful solutions.

One powerful feature in C++ that allows for the combination of OOP and FP techniques is **functors**. Functors are objects that can be treated like functions. They encapsulate both data and behavior, allowing for abstraction and code reuse, similar to classes in OOP. At the same time, functors can be invoked like functions and passed around as arguments, just like in FP.

## Creating a Functor in C++

In C++, functors can be created by overloading the `operator()` method in a custom class. This allows instances of the class to be called like functions. Let's take a look at an example:

```cpp
class AddFunctor
{
public:
    int operator()(int a, int b)
    {
        return a + b;
    }
};
```

In the code example above, we define a functor named `AddFunctor`. It has an `operator()` method which takes two integers as parameters and returns their sum. Notice how the instance of this functor can be invoked like a function:

```cpp
AddFunctor add;
int result = add(2, 3); // result = 5
```

## Using Functors for Flexible Functionality

One of the advantages of functors is the ability to pass them as arguments to other functions. This allows for dynamic behavior and flexibility in code. Consider the following example:

```cpp
class GreaterThanFunctor
{
public:
    bool operator()(int a, int b)
    {
        return a > b;
    }
};

bool containsGreaterThan(const std::vector<int>& nums, GreaterThanFunctor functor)
{
    for (int num : nums)
    {
        if (functor(num, 10))
        {
            return true;
        }
    }
    return false;
}
```

In this example, we define a functor `GreaterThanFunctor` that checks if a number is greater than a given value. The `containsGreaterThan` function takes a vector of numbers and a functor as arguments. It iterates through the numbers and uses the functor to determine if any number is greater than 10.

```cpp
std::vector<int> numbers = {5, 12, 8, 3};

GreaterThanFunctor functor;
bool result = containsGreaterThan(numbers, functor); // result = true
```

## Conclusion

Functors in C++ provide a way to combine elements of object-oriented and functional programming paradigms. They offer the power of abstraction and code reuse from OOP, while allowing for dynamic behavior and flexibility from FP. By using functors, you can write more expressive and flexible code that adapts to different situations.

#cpp #functors