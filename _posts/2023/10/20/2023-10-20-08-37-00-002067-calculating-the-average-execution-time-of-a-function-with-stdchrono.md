---
layout: post
title: "Calculating the average execution time of a function with std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In this article, we will explore how to calculate the average execution time of a function using the `std::chrono` library in C++. Calculating the average execution time of a function is useful when we want to measure the performance of our code and identify any potential bottlenecks.

#### Table of Contents
- [Introduction](#introduction)
- [Calculating Execution Time](#calculating-execution-time)
- [Calculating Average Execution Time](#calculating-average-execution-time)
- [Example](#example)
- [Conclusion](#conclusion)


#### Introduction
`std::chrono` is a library in C++ that provides facilities for measuring time durations and time points. It allows us to accurately measure the execution time of a function by capturing the starting and ending time points.

#### Calculating Execution Time
To calculate the execution time of a function, we need to capture the starting and ending time points using `std::chrono` high-resolution clocks. Here's a simple example:

```cpp
#include <chrono>

void myFunction()
{
    // Function logic
}

int main()
{
    // Start time point
    auto start = std::chrono::high_resolution_clock::now();

    // Call the function
    myFunction();

    // End time point
    auto end = std::chrono::high_resolution_clock::now();

    // Calculate execution time
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start);

    // Print execution time in microseconds
    std::cout << "Execution Time: " << duration.count() << " microseconds" << std::endl;

    return 0;
}
```

In the above example, we use `std::chrono::high_resolution_clock` to capture the starting and ending time points before and after calling the function `myFunction()`. We calculate the duration between these time points and print it as the execution time of the function.

#### Calculating Average Execution Time
To calculate the average execution time, we can run the function multiple times and calculate the average of the durations. Here's an example of how to do that:

```cpp
#include <chrono>

void myFunction()
{
    // Function logic
}

int main()
{
    int numIterations = 10; // Number of times to run the function
    double sumDurations = 0;

    for (int i = 0; i < numIterations; ++i)
    {
        auto start = std::chrono::high_resolution_clock::now();
        myFunction();
        auto end = std::chrono::high_resolution_clock::now();

        auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start);
        sumDurations += duration.count();

        std::cout << "Execution Time (Iteration " << i + 1 << "): " << duration.count() << " microseconds" << std::endl;
    }

    double averageDuration = sumDurations / numIterations;
    std::cout << "Average Execution Time: " << averageDuration << " microseconds" << std::endl;

    return 0;
}
```

In the above example, we run the function `myFunction()` `numIterations` times in a loop. We calculate the duration for each iteration and sum them up. Finally, we calculate the average duration by dividing the sum by the number of iterations.

#### Example
Let's consider an example where we want to calculate the average execution time of a function that sorts an array of integers using the bubble sort algorithm. Here's the code:

```cpp
#include <iostream>
#include <chrono>
#include <random>

void bubbleSort(int arr[], int size)
{
    for (int i = 0; i < size - 1; ++i)
    {
        for (int j = 0; j < size - i - 1; ++j)
        {
            if (arr[j] > arr[j + 1])
            {
                std::swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main()
{
    int numElements = 10000;
    int numIterations = 10;

    double sumDurations = 0;

    // Create a random number generator
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dis(1, 1000);

    for (int i = 0; i < numIterations; ++i)
    {
        int arr[numElements];

        // Fill array with random numbers
        for (int j = 0; j < numElements; ++j)
        {
            arr[j] = dis(gen);
        }

        auto start = std::chrono::high_resolution_clock::now();
        bubbleSort(arr, numElements);
        auto end = std::chrono::high_resolution_clock::now();

        auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start);
        sumDurations += duration.count();

        std::cout << "Execution Time (Iteration " << i + 1 << "): " << duration.count() << " microseconds" << std::endl;
    }

    double averageDuration = sumDurations / numIterations;
    std::cout << "Average Execution Time: " << averageDuration << " microseconds" << std::endl;

    return 0;
}
```

In the above example, we generate an array of 10,000 random integers and sort it using the bubble sort algorithm. We run the sorting process 10 times and calculate the average execution time.

#### Conclusion
By using the `std::chrono` library in C++, we can accurately measure the execution time of a function and calculate its average execution time. This allows us to analyze the performance of our code and identify any optimizations that can be made. Calculating the average execution time is a valuable technique when it comes to improving the efficiency of our programs.

Make sure to follow the guidelines provided in the C++ standard library documentation for accurate and precise time measurements.

*Tags: #C++ #std::chrono*