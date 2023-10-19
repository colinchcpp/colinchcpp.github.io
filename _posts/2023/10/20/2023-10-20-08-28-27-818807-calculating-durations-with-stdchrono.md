---
layout: post
title: "Calculating durations with std::chrono"
description: " "
date: 2023-10-20
tags: [references]
comments: true
share: true
---

When working with time and durations in C++, the `<chrono>` library comes in handy. This library provides a high-level interface for dealing with time-related operations, including calculating durations.

## Calculating Durations

To calculate durations using `std::chrono`, you need to work with two main types: `std::chrono::time_point` and `std::chrono::duration`. 

### `std::chrono::time_point`

A `time_point` represents a point in time and is defined by a clock. You can think of it as a timestamp. The `<chrono>` library includes multiple clock types, such as `std::chrono::system_clock` and `std::chrono::high_resolution_clock`, among others. 

Here's an example of creating a `time_point` using the `system_clock`:

```cpp
#include <chrono>

std::chrono::time_point<std::chrono::system_clock> start = std::chrono::system_clock::now();
```

In this example, the variable `start` is initialized with the current time using the `now()` function of the `system_clock`.

### `std::chrono::duration`

A `duration` represents a time span. It is defined by the number of ticks and the tick period. The `<chrono>` library provides different duration types such as `std::chrono::duration`, `std::chrono::milliseconds`, and `std::chrono::hours`, to name a few.

To calculate the duration between two `time_point` objects, you subtract one from the other. Here's an example:

```cpp
std::chrono::time_point<std::chrono::system_clock> end = std::chrono::system_clock::now();

std::chrono::duration<double> elapsed_seconds = end - start;
```

In this example, `end` is another `time_point` initialized with the current time. Subtracting `start` from `end` gives us a `duration`, which represents the elapsed time in seconds (as a floating-point value).

## Working with Durations

Once you have a `duration`, you can perform various operations on it. The `std::chrono::duration` type provides member functions to get the count of ticks and convert durations to different units.

Here are a few examples:

```cpp
double seconds = elapsed_seconds.count(); // Get the duration in seconds

// Convert duration to milliseconds
std::chrono::milliseconds elapsed_milliseconds = std::chrono::duration_cast<std::chrono::milliseconds>(elapsed_seconds);
int milliseconds = elapsed_milliseconds.count();

// Convert duration to microseconds
std::chrono::microseconds elapsed_microseconds = std::chrono::duration_cast<std::chrono::microseconds>(elapsed_seconds);
int microseconds = elapsed_microseconds.count();
```

In the above examples, we use the `count()` function to get the count of ticks for the duration. We also utilize `std::chrono::duration_cast` to convert the duration to different time units.

## Conclusion

With the `<chrono>` library, calculating durations in C++ becomes straightforward. By working with `time_point` and `duration` objects, you can accurately measure and manipulate time-related operations in your code. It's a powerful tool when dealing with tasks that involve timing, profiling, or benchmarking.

#references
- [C++ Reference - <chrono> library](https://en.cppreference.com/w/cpp/chrono)
- [cplusplus.com - Chrono library in C++](http://www.cplusplus.com/reference/chrono/)