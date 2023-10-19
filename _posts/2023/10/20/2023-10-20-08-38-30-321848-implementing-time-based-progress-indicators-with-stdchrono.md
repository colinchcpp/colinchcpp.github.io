---
layout: post
title: "Implementing time-based progress indicators with std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

When working on long-running tasks or processes, it is often helpful to provide a progress indicator to give users an idea of how much time is remaining. One way to achieve this is by using the `std::chrono` library in C++.

## Getting started with std::chrono

`std::chrono` is a library that provides a set of type-safe and thread-safe functions for handling time-related operations in C++. It was introduced in the C++11 standard and offers convenient facilities for measuring time durations and time points.

To use `std::chrono`, you first need to include the `<chrono>` header file:

```cpp
#include <chrono>
```

## Measuring time duration

To implement a time-based progress indicator, you need to measure the duration of the task. You can do this by using the `std::chrono::steady_clock` and `std::chrono::duration` classes.

Here's an example of how to measure the duration of a task:

```cpp
#include <iostream>
#include <chrono>

int main() {
    auto start = std::chrono::steady_clock::now();
    
    // Perform the task
    
    auto end = std::chrono::steady_clock::now();
    
    auto duration = std::chrono::duration_cast<std::chrono::seconds>(end - start).count();
    
    std::cout << "Task took " << duration << " seconds." << std::endl;
    
    return 0;
}
```

In this example, `std::chrono::steady_clock::now()` is used to get the current time before and after the task. The duration is then calculated by subtracting the start time from the end time. The `std::chrono::duration_cast` function is used to convert the duration to seconds, and `count()` gives the numeric value of the duration.

## Implementing a time-based progress indicator

Now that we can measure the duration of a task, let's implement a time-based progress indicator. We will use a combination of a progress bar and the estimated time remaining.

Here's a basic implementation:

```cpp
#include <iostream>
#include <chrono>

void updateProgress(float progress) {
    int barWidth = 40;
    
    std::cout << "[";
    int pos = static_cast<int>(barWidth * progress);
    for (int i = 0; i < barWidth; ++i) {
        if (i < pos) std::cout << "=";
        else if (i == pos) std::cout << ">";
        else std::cout << " ";
    }
    std::cout << "] " << int(progress * 100.0) << "%\r";
    std::cout.flush();
}

int main() {
    int totalIterations = 100;
    auto start = std::chrono::steady_clock::now();
    
    for (int i = 0; i <= totalIterations; ++i) {
        // Perform a task
        
        float progress = static_cast<float>(i) / totalIterations;
        updateProgress(progress);
    }
    
    auto end = std::chrono::steady_clock::now();
    
    auto duration = std::chrono::duration_cast<std::chrono::seconds>(end - start).count();
    
    std::cout << "\nTask took " << duration << " seconds." << std::endl;
    
    return 0;
}
```

In this example, we have a `updateProgress` function that takes a `progress` value between 0.0 and 1.0. It updates the progress bar and displays the progress as a percentage.

When running the task in a loop, we calculate the progress at each iteration and call the `updateProgress` function to display the progress.

## Conclusion

By utilizing the `std::chrono` library in C++, you can easily implement time-based progress indicators for your long-running tasks or processes. This provides a visual representation of progress, making it easier for users to understand how much time is remaining. Feel free to customize and enhance the progress indicator implementation to fit your specific requirements.

# References

- [C++ reference - std::chrono](https://en.cppreference.com/w/cpp/header/chrono)