---
layout: post
title: "Calculating the execution time of nested loops using std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

When working with nested loops, it's often necessary to measure the execution time to evaluate the efficiency and performance of your code. C++ provides the `std::chrono` library, which allows you to accurately measure time durations.

In this tutorial, we will demonstrate how to calculate the execution time of nested loops using `std::chrono`.

## Table of Contents
- [Using std::chrono](#using-stdchrono)
- [Measuring Execution Time](#measuring-execution-time)
- [Example Code](#example-code)
- [Conclusion](#conclusion)

## Using std::chrono

The `std::chrono` library provides a variety of time-related classes and functions to work with. The most commonly used classes include `std::chrono::system_clock`, `std::chrono::steady_clock`, and `std::chrono::high_resolution_clock`. For measuring execution time, we will use `std::chrono::high_resolution_clock` as it provides the highest resolution available on your system.

## Measuring Execution Time

To measure the execution time of nested loops, we need to record the starting and ending time points and then calculate the duration in between.

Here are the steps to measure the execution time using `std::chrono`:

1. Include the necessary header for `std::chrono`:

```cpp
#include <chrono>
```

2. Declare variables for the starting and ending time points:

```cpp
std::chrono::high_resolution_clock::time_point start, end;
```

3. Capture the starting time point before the nested loops:

```cpp
start = std::chrono::high_resolution_clock::now();
```

4. Execute the nested loops:

```cpp
for (int i = 0; i < outerLoopCount; i++) {
    for (int j = 0; j < innerLoopCount; j++) {
        // Code inside the nested loops
    }
}
```

5. Capture the ending time point after the nested loops:

```cpp
end = std::chrono::high_resolution_clock::now();
```

6. Calculate the duration between the starting and ending time points:

```cpp
auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start);
```

7. Output the calculated duration:

```cpp
std::cout << "Execution time: " << duration.count() << " microseconds" << std::endl;
```

By following these steps, we can accurately measure the execution time of nested loops using `std::chrono`.

## Example Code

Here is an example code snippet that demonstrates the measurement of execution time:

```cpp
#include <iostream>
#include <chrono>

int main() {
    const int outerLoopCount = 1000;
    const int innerLoopCount = 10000;

    std::chrono::high_resolution_clock::time_point start, end;
    start = std::chrono::high_resolution_clock::now();

    for (int i = 0; i < outerLoopCount; i++) {
        for (int j = 0; j < innerLoopCount; j++) {
            // Code inside the nested loops
        }
    }

    end = std::chrono::high_resolution_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start);

    std::cout << "Execution time: " << duration.count() << " microseconds" << std::endl;

    return 0;
}
```

## Conclusion

Measuring the execution time of nested loops is essential for performance analysis. By using `std::chrono` in C++, you can accurately measure the duration of your code. Remember to capture the starting and ending time points and calculate the duration using `std::chrono::duration_cast`.