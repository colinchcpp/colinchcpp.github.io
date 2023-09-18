---
layout: post
title: "Utilizing functors for multi-threaded programming in C++"
description: " "
date: 2023-09-14
tags: [MultiThreading]
comments: true
share: true
---

In multi-threaded programming, functors can be a powerful tool to achieve parallel execution and improve the performance of your C++ code. Functors, also known as function objects, are objects that can be invoked like a function.

## What is a Functor?

A functor is a class or a struct that overloads the `operator()` function. This allows objects of the class to be invoked as if they were regular functions. Functors can hold state and can be passed as arguments or stored in variables, making them versatile for multi-threaded programming.

## Benefits of Using Functors in Multi-threading

1. **Parallel Execution**: Functors can be used as task objects to be executed concurrently by multiple threads. By dividing the workload into smaller tasks and assigning them to threads, you can achieve parallel execution and reduce overall processing time.

2. **Shared State Access**: Functors can have member variables that can be shared across multiple threads. This allows different threads to access and modify shared data in a synchronized manner, ensuring thread safety.

3. **Flexibility**: Functors can be customized to fit your specific needs. You can define your own operators and member variables to control the behavior of the functor and optimize the multi-threaded execution.

## Example: Multi-threaded Sum Calculation using Functors

Let's see an example of utilizing functors for multi-threaded sum calculation using C++11's `std::thread`. This example calculates the sum of an array using multiple threads.

```cpp
#include <iostream>
#include <thread>
#include <vector>

class SumCalculator {
public:
    SumCalculator(const std::vector<int>& numbers) : numbers(numbers), sum(0) {}

    void operator()(int start, int end) {
        for (int i = start; i < end; ++i) {
            sum += numbers[i];
        }
    }

    int getSum() const {
        return sum;
    }

private:
    const std::vector<int>& numbers;
    int sum;
};

int main() {
    std::vector<int> numbers{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    const int threadCount = 4;
    const int chunkSize = numbers.size() / threadCount;

    std::vector<std::thread> threads;
    std::vector<SumCalculator> calculators;

    for (int i = 0; i < threadCount; ++i) {
        int start = i * chunkSize;
        int end = start + chunkSize;

        if (i == threadCount - 1) {
            end = numbers.size();
        }

        calculators.emplace_back(numbers);
        threads.emplace_back(calculators[i], start, end);
    }

    for (auto& thread : threads) {
        thread.join();
    }

    int totalSum = 0;
    for (const auto& calculator : calculators) {
        totalSum += calculator.getSum();
    }

    std::cout << "Sum: " << totalSum << std::endl;

    return 0;
}
```

In this example, we define a `SumCalculator` functor class that holds the input array and the sum as member variables. The `operator()` function is overloaded to handle the summation of a portion of the array. We create multiple instances of the `SumCalculator` functor, each responsible for calculating the sum of a specific portion of the array. These instances are executed in parallel using separate threads.

By dividing the array into multiple chunks and assigning each chunk to a separate thread, we achieve parallel execution. After all the threads have finished execution, we collect the individual sums calculated by each `SumCalculator` instance and compute the total sum.

## Conclusion

Utilizing functors for multi-threaded programming in C++ can help you achieve parallel execution and optimize the performance of your code. Functors provide a flexible and efficient way to divide workloads and share state across multiple threads. By designing your own functors, you can tailor them to fit your specific needs and enhance the efficiency of your multi-threaded applications.

#C++ #MultiThreading