---
layout: post
title: "Lambdas with capture initialization for controlling the lifetime of captured variables"
description: " "
date: 2023-10-13
tags: [Capture]
comments: true
share: true
---

Lambda functions in programming are powerful tools for creating anonymous functions that can be used inline with other code. They have the ability to capture variables from their surrounding environment. In C++, lambdas can also take advantage of capture initialization to control the lifetime of captured variables. 

## What is Capture Initialization?

Capture initialization is a feature in C++ that allows you to control the lifetime of captured variables within a lambda function. By using capture initialization, you can specify how variables should be captured, whether by value or by reference, and also control the way they are initialized.

## Capturing Variables by Value

When capturing variables by value, a copy of the captured variable is made and stored within the lambda function. This means that any changes made to the captured variable inside the lambda will not affect the original variable outside of the lambda.

```cpp
int x = 10;

auto lambda = [y = x]() {
    std::cout << y << std::endl; // Prints 10
    y = 20;
    std::cout << y << std::endl; // Prints 20
};

x = 30;

lambda();
std::cout << x << std::endl; // Prints 30
```

In the example above, we capture the variable `x` by value and assign it to a new variable `y` inside the lambda. Any changes made to `y` will not affect `x` outside of the lambda.

## Capturing Variables by Reference

Capturing variables by reference allows the lambda to access and modify the original variable outside of the lambda. However, you need to be careful as the referenced variable must outlive the lambda itself.

```cpp
int x = 10;

auto lambda = [&y = x]() {
    std::cout << y << std::endl; // Prints 10
    y = 20;
    std::cout << y << std::endl; // Prints 20
};

lambda();
std::cout << x << std::endl; // Prints 20
```

In the example above, we capture the variable `x` by reference and assign it to `y` inside the lambda. Any changes made to `y` will also affect `x` outside of the lambda.

## Controlling Initialization of Captured Variables

Capture initialization also gives you control over how captured variables are initialized. You can use braces `{}` to specify the initialization expression.

```cpp
auto lambda = [number = computeNumber()]() {
    std::cout << number << std::endl;
};

lambda();
```

In the example above, we initialize the captured variable `number` by calling the `computeNumber()` function. This allows us to capture the result of the function call and use it inside the lambda.

## Conclusion

Capture initialization in lambdas provides additional flexibility and control over the lifetime of captured variables in C++. By capturing variables by value or reference and controlling their initialization, you can better tailor the behavior of your lambda functions to suit your needs.

# References
- [C++ Lambdas](https://en.cppreference.com/w/cpp/language/lambda)
- [Capture Initialization in C++](https://en.cppreference.com/w/cpp/language/lambda#Capture_init)