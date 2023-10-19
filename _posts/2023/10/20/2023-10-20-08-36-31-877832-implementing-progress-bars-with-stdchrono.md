---
layout: post
title: "Implementing progress bars with std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In many applications, displaying a progress bar is a great way to provide visual feedback to the user about the progress of a lengthy task. In this blog post, we will explore how to implement progress bars using the std::chrono library in C++.

## Table of Contents
- [Introduction](#introduction)
- [Implementation](#implementation)
- [Example Usage](#example-usage)
- [Conclusion](#conclusion)

## Introduction

The std::chrono library in C++ provides facilities for working with time durations, clocks, and timestamps. We can leverage this library to create a progress bar that updates dynamically based on the elapsed time.

## Implementation

To implement a progress bar using std::chrono, we need to calculate the elapsed time and update the progress bar accordingly. Here's an example implementation:

```cpp
#include <iostream>
#include <chrono>
#include <thread>

void updateProgress(int progress) {
    std::cout << "\rProgress: " << progress << "% ";
    std::cout.flush();
}

void simulateLengthyTask() {
    int total = 100;
    for (int i = 0; i <= total; i++) {
        updateProgress((i * 100) / total);
        std::this_thread::sleep_for(std::chrono::milliseconds(100)); // Simulate some work
    }
    std::cout << std::endl;
}

int main() {
    auto startTime = std::chrono::system_clock::now();
    
    simulateLengthyTask();
    
    auto endTime = std::chrono::system_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::seconds>(endTime - startTime).count();
    
    std::cout << "Time taken: " << duration << " seconds" << std::endl;
    
    return 0;
}
```

In this implementation, we have two helper functions: `updateProgress()` and `simulateLengthyTask()`. The `updateProgress()` function updates the progress bar by printing the current progress percentage. The `simulateLengthyTask()` function performs some work and updates the progress bar after each iteration.

In the `main()` function, we calculate the elapsed time by subtracting the `startTime` from the `endTime` using std::chrono. We then print the total time taken.

## Example Usage

To use the progress bar implementation, simply call the `simulateLengthyTask()` function within your application. The progress bar will update dynamically, providing visual feedback to the user about the progress of the task. After the task completes, the total time taken will be printed.

## Conclusion

Implementing progress bars using std::chrono in C++ is a straightforward way to provide visual feedback to users about the progress of lengthy tasks. By leveraging the std::chrono library, we can easily calculate the elapsed time and update the progress bar accordingly.