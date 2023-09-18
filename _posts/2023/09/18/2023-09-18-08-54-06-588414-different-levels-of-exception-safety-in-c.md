---
layout: post
title: "Different levels of exception safety in C++"
description: " "
date: 2023-09-18
tags: [CPlusPlus, ExceptionSafety]
comments: true
share: true
---

1. **No-throw guarantee (nothrow)**: This level of exception safety guarantees that a function will never throw an exception. It is typically achieved by using techniques such as checking preconditions or using error codes instead of exceptions. This level of safety is especially useful when dealing with critical operations such as resource allocation.

2. **Basic guarantee**: This level of exception safety ensures that if an exception is thrown, the program is left in a valid and consistent state, with no memory leaks. It typically involves using exception handling mechanisms such as `try-catch` blocks to catch and handle exceptions appropriately. However, the state of the program might not be exactly the same as before the exception was thrown.

3. **Strong guarantee**: This is the highest level of exception safety. It guarantees that if an exception is thrown, the program state remains unchanged. It achieves this by using techniques such as transactional operations, where all changes are made atomically and can be rolled back if an exception occurs. The strong guarantee ensures that the program behaves as if the operation never took place if an exception is thrown.

It's important to note that achieving a higher level of exception safety often comes at the cost of performance or code complexity. Developers should carefully consider the trade-offs and choose the appropriate level of exception safety based on the requirements of their program.

In conclusion, exception safety is an essential aspect of writing reliable C++ code. By understanding and implementing different levels of exception safety, developers can create robust programs that handle exceptions gracefully and prevent unwanted side effects. #CPlusPlus #ExceptionSafety