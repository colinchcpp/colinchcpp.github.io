---
layout: post
title: "Calculating the execution time of mathematical computations using std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In any programming language, it is important to measure the execution time of our code to optimize performance and understand any potential bottlenecks. C++ provides a high-resolution clock facility through the `std::chrono` library, which we can leverage to measure the time taken for mathematical computations.

## Including the necessary header files

First, we need to include the required header file, `chrono`, to utilize the `std::chrono` library:

```cpp
#include <chrono>
```

## Using std::chrono to measure execution time

To measure the execution time of a specific block of code, we can follow these steps:

1. Define a `std::chrono::high_resolution_clock` object before the code block that we want to measure:

```cpp
std::chrono::high_resolution_clock::time_point startTime = std::chrono::high_resolution_clock::now();
```

2. Perform the mathematical computations or code that we want to measure.

3. Define another `std::chrono::high_resolution_clock` object after the code block:

```cpp
std::chrono::high_resolution_clock::time_point endTime = std::chrono::high_resolution_clock::now();
```

4. Calculate the duration by subtracting the start time from the end time:

```cpp
auto duration = std::chrono::duration_cast<std::chrono::microseconds>(endTime - startTime).count();
```

Here, we've used `std::chrono::duration_cast` to obtain the duration in microseconds. You can also choose other units such as milliseconds, seconds, etc., depending on your specific requirements.

## Example usage

Let's consider an example where we want to measure the execution time of a function that calculates the nth Fibonacci number using the recursive approach:

```cpp
#include <iostream>
#include <chrono>

int fibonacci(int n) {
    if (n <= 1)
        return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n = 30;
    
    std::chrono::high_resolution_clock::time_point startTime = std::chrono::high_resolution_clock::now();
    
    int result = fibonacci(n);
    
    std::chrono::high_resolution_clock::time_point endTime = std::chrono::high_resolution_clock::now();
    
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(endTime - startTime).count();
    
    std::cout << "Fibonacci(" << n << ") = " << result << std::endl;
    std::cout << "Execution time: " << duration << " microseconds." << std::endl;
    
    return 0;
}
```

In the above example, we measure the execution time of the `fibonacci` function by calculating the 30th Fibonacci number. The result and execution time are then printed to the console.

## Conclusion

By utilizing the `std::chrono` library in C++, we can accurately measure the execution time of mathematical computations or any other code blocks. This allows us to optimize our programs and identify potential performance improvements.