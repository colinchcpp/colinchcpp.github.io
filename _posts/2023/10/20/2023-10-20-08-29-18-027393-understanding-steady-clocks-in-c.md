---
layout: post
title: "Understanding steady clocks in C++"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

When it comes to measuring time in C++, one of the most reliable and accurate methods is to use steady clocks. Steady clocks provide a stable and consistent reference point, typically with a resolution of nanoseconds. In this blog post, we will explore what steady clocks are, how to use them in C++, and some practical examples.

## Table of Contents
- [Overview of steady clocks](#overview-of-steady-clocks)
- [Using steady clocks in C++](#using-steady-clocks-in-c)
- [Practical examples](#practical-examples)
- [Conclusion](#conclusion)

## Overview of steady clocks

A steady clock is a type of clock that guarantees a monotonic progression of time, meaning it never goes backward. This is crucial when measuring time intervals, as it ensures accurate and consistent results. Steady clocks are preferred over system clocks or high-resolution clocks, which may be subject to adjustments due to factors like clock drift or system time changes.

In C++, the `<chrono>` library provides the `steady_clock` type, which represents a steady clock. It uses the highest resolution clock available on the system and ensures a steady time progression.

## Using steady clocks in C++

To start using steady clocks in your C++ code, you need to include the `<chrono>` header and use the `std::chrono::steady_clock` type. Here's an example of measuring the execution time of a code snippet:

```cpp
#include <iostream>
#include <chrono>

int main() {
    auto start = std::chrono::steady_clock::now();

    // Code snippet to measure execution time

    auto end = std::chrono::steady_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count();

    std::cout << "Execution time: " << duration << " milliseconds" << std::endl;

    return 0;
}
```

In the example above, we capture the start time using `std::chrono::steady_clock::now()`. After executing the code snippet, we capture the end time using the same function. We then calculate the duration by subtracting the start time from the end time and convert it to milliseconds using `std::chrono::duration_cast`. Finally, we print the execution time.

## Practical examples

Steady clocks are useful for various time-related applications, such as performance profiling, measuring algorithm execution time, and benchmarking. Here are a few practical examples:

### Timing a function call

```cpp
#include <iostream>
#include <chrono>

void myFunction() {
    // Code to be timed
}

int main() {
    auto start = std::chrono::steady_clock::now();

    myFunction();

    auto end = std::chrono::steady_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start).count();

    std::cout << "Function execution time: " << duration << " microseconds" << std::endl;

    return 0;
}
```

### Measuring loop execution time

```cpp
#include <iostream>
#include <chrono>

int main() {
    auto start = std::chrono::steady_clock::now();

    for (int i = 0; i < 1000000; ++i) {
        // Code inside the loop
    }

    auto end = std::chrono::steady_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count();

    std::cout << "Loop execution time: " << duration << " milliseconds" << std::endl;

    return 0;
}
```

## Conclusion

Steady clocks in C++ provide a reliable and accurate way to measure time intervals without the risk of inconsistencies caused by factors like clock drift. By using the `std::chrono::steady_clock` type from the `<chrono>` library, you can easily measure the execution time of code snippets, functions, or loops. Steady clocks are a valuable tool for performance optimization, algorithm analysis, and profiling in C++.