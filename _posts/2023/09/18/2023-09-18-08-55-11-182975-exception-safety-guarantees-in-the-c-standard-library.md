---
layout: post
title: "Exception safety guarantees in the C++ standard library"
description: " "
date: 2023-09-18
tags: [ExceptionSafety]
comments: true
share: true
---

When working with the C++ standard library, it is important to understand the exception safety guarantees provided by various functions and classes. Exception safety is the concept of ensuring that program state remains consistent and resources are not leaked when an exception is thrown. This is crucial for writing robust and reliable code that can handle unexpected errors gracefully.

The C++ standard library provides three levels of exception safety guarantees:

1. **No-throw guarantee**: Functions with this guarantee will not throw any exceptions. They are completely immune to exceptions and do not alter the program's state. This level of exception safety is assured for operations like `std::swap` and accessor functions like `std::vector::size`.

2. **Basic guarantee**: Functions with this guarantee ensure that if an exception is thrown, the program state remains consistent and no resources are leaked. The objects being operated on may be left in a valid but unspecified state. Most operations in the standard library provide this level of exception safety. For example, `std::vector::push_back` will not leak memory if an exception occurs, but the vector may be left with a different state.

3. **Strong guarantee**: Functions with this guarantee provide a strong exception safety guarantee. If an exception is thrown, the program state and resources used by the operation are rolled back to the state before the operation was started. The objects remain unchanged in case of exceptions. Functions that offer this level of exception safety usually use a technique called **copy and swap idiom**. `std::vector::emplace_back` provides a strong guarantee because it creates a temporary object and only swaps it in if the operation succeeds.

Understanding the exception safety guarantees for different operations in the C++ standard library allows developers to write code that can handle exceptions properly and ensure program integrity. It is important to note that while the standard library strives to provide exception safety, it is also the responsibility of the developer to handle exceptions appropriately and design their own code with exception safety in mind.

#C++ #ExceptionSafety