---
layout: post
title: "Building timers for games and animations using std::chrono"
description: " "
date: 2023-10-20
tags: [gamedevelopment, animation]
comments: true
share: true
---

In game development and animation, timers are essential to control the flow of events and create dynamic experiences. C++ provides the `std::chrono` library, which offers a high-resolution clock for accurate timing. In this blog post, we will explore how to build timers for games and animations using `std::chrono`.

## Table of Contents
- [Introduction to std::chrono](#introduction-to-stdchrono)
- [Creating a timer](#creating-a-timer)
- [Updating the timer](#updating-the-timer)
- [Pausing and resuming the timer](#pausing-and-resuming-the-timer)
- [Conclusion](#conclusion)

## Introduction to std::chrono

`std::chrono` is a C++ library introduced in the C++11 standard, providing utilities for time-related operations. It offers a flexible and easy-to-use way to measure time intervals and perform calculations with time points.

The library includes different clock types, such as `system_clock`, `steady_clock`, and `high_resolution_clock`, each suited for specific use cases. When building timers for games and animations, the `high_resolution_clock` is often the best choice due to its high precision.

## Creating a timer

To create a timer using `std::chrono`, we need to store the start time point and the duration of the timer. We can define our timer class and include the necessary headers:

```cpp
#include <chrono>

class Timer {
public:
    using Clock = std::chrono::high_resolution_clock;
    using TimePoint = std::chrono::time_point<Clock>;

    Timer() {
        start();
    }

    void start() {
        start_time_ = Clock::now();
    }
    
private:
    TimePoint start_time_;
};
```

In the example above, we define a class called `Timer` that uses `std::chrono::high_resolution_clock` as the clock type. The `TimePoint` type represents a point in time.

The constructor of the `Timer` class automatically starts the timer by calling the `start` function, which sets the `start_time_` variable to the current time using `Clock::now()`.

## Updating the timer

Next, we need to update our timer to calculate the elapsed time. We can add a member function called `getElapsedTime` to calculate the duration between the start time and the current time:

```cpp
class Timer {
public:
    // ...

    std::chrono::milliseconds getElapsedTime() const {
        auto current_time = Clock::now();
        return std::chrono::duration_cast<std::chrono::milliseconds>(current_time - start_time_);
    }

private:
    // ...
};
```

The `getElapsedTime` function subtracts the start time from the current time and converts the duration to milliseconds using `std::chrono::duration_cast`.

## Pausing and resuming the timer

In games and animations, it is often necessary to pause and resume timers. We can add member functions to pause and resume our timer:

```cpp
class Timer {
public:
    // ...

    void pause() {
        paused_ = true;
        pause_time_ = Clock::now();
    }

    void resume() {
        if (paused_) {
            auto resume_time = Clock::now();
            start_time_ += (resume_time - pause_time_);
            paused_ = false;
        }
    }

private:
    // ...
};
```

The `pause` function sets the `paused_` flag to true and saves the current time in `pause_time_`. The `resume` function checks if the timer is paused and adjusts the start time accordingly.

## Conclusion

By utilizing the `std::chrono` library in C++, we can easily create timers for games and animations. The high-resolution clock provides accurate timing, and the various functionalities allow control over pausing and resuming the timers as needed.

Remember to check the [official documentation](https://en.cppreference.com/w/cpp/chrono) for more details on `std::chrono` and its available features.

#gamedevelopment #animation