---
layout: post
title: "Functors vs. lambdas in C++: pros and cons"
description: " "
date: 2023-09-14
tags: [FunctorsVsLambdas]
comments: true
share: true
---

In C++, there are multiple ways to implement function objects: by using functors or lambdas. Both functors and lambdas serve a similar purpose, but there are significant differences between the two. In this blog post, we will explore the pros and cons of using functors and lambdas in C++.

## Functors

A functor is a class or struct that overloads the function call operator `operator()`. It allows objects to be used as if they were functions. Functors have been a part of C++ since its early days and offer several advantages:

**1. Flexibility:** Functors can store internal state by using member variables, which allows them to maintain a particular state across multiple function calls. This can be useful for situations where the same function object needs to be called repeatedly with different arguments.

**2. Reusability:** Functors can be used in different contexts and scenarios. Since they are regular objects, they can be created, copied, and passed as arguments to functions.

**3. Compatibility:** Functors are compatible with C++03 and earlier versions, making them suitable for projects that require backward compatibility.

However, there are also some drawbacks to using functors:

**1. Syntax and verbosity:** Functors require defining separate classes, which can make the code more verbose and less readable compared to other alternatives.

**2. Limited expressiveness:** Functors can be limited in terms of expressiveness, especially when dealing with complex, one-off functions that don't need to be reused.

## Lambdas

Introduced in C++11, lambdas provide a more concise and expressive way to define anonymous functions. Lambdas have become increasingly popular due to their ability to capture variables from the enclosing scope. Here are some advantages of using lambdas:

**1. Conciseness:** Lambdas allow you to define functions inline, reducing the need for creating separate classes.

**2. Readability:** By eliminating the need for separate class definitions, lambdas make the code more concise and easier to read, especially for small, one-off functions.

**3. Capturing variables:** Lambdas can capture variables from the enclosing scope, allowing them to be used within the lambda function.

However, there are some considerations to keep in mind while using lambdas:

**1. Inability to maintain state:** Unlike functors, lambdas cannot store internal state. They are limited to capturing and using variables from the enclosing scope.

**2. Code duplication:** Since lambdas are anonymous functions, they cannot be reused directly in multiple places. Code duplication may occur if the same lambda functionality is needed in different parts of the code.

To summarize, both functors and lambdas have their own advantages and disadvantages. Functors provide more flexibility and reusability, making them suitable for scenarios that require maintaining internal state or backward compatibility. On the other hand, lambdas offer concise syntax and the ability to capture variables from the enclosing scope, making them a great choice for small, one-off functions.

#C++ #FunctorsVsLambdas