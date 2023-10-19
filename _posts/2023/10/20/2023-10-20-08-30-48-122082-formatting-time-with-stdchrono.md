---
layout: post
title: "Formatting time with std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

One common task in programming is to format time in a specific way. The C++ standard library provides the `std::chrono` library which is a powerful and flexible tool for dealing with time-related operations.

In this blog post, we will explore how to use `std::chrono` to format time in various ways, such as converting it to a string or extracting individual time components.

## Formatting time as a string

To format time as a string, we can make use of the `std::put_time` function from the `<iomanip>` header. This function allows us to format a `std::chrono::time_point` object into a string using a format specifier.

Here's an example to format the current local time as a string:

```cpp
#include <iostream>
#include <iomanip>
#include <chrono>

int main() {
    auto current_time = std::chrono::system_clock::to_time_t(std::chrono::system_clock::now());
    std::cout << std::put_time(std::localtime(&current_time), "%F %T") << std::endl;
    return 0;
}
```

In this example, we retrieve the current local time as a `std::chrono::time_point` object using `std::chrono::system_clock::now()`. We then convert it to a `std::time_t` object using `std::chrono::system_clock::to_time_t()`. Finally, we pass this `std::time_t` object to `std::put_time` along with the desired format specifier ("%F %T") to get the formatted string representation of the time.

The output of the above example might look like: "2022-05-28 15:30:00".

## Extracting individual time components

`std::chrono` also provides various facilities to extract individual time components such as hours, minutes, and seconds from a `std::chrono::time_point`.

Here's an example to extract the current hour from the local time:

```cpp
#include <iostream>
#include <chrono>

int main() {
    auto current_time = std::chrono::system_clock::to_time_t(std::chrono::system_clock::now());
    auto local_time = *std::localtime(&current_time);
    auto hour = local_time.tm_hour;
    std::cout << "Current hour: " << hour << std::endl;
    return 0;
}
```

In this example, we retrieve the current local time as a `std::chrono::time_point` object and then convert it to a `std::time_t` object. We then use `std::localtime` to convert the `std::time_t` object into a `std::tm` object which represents the local time. Finally, we access the `tm_hour` member of `std::tm` to get the current hour.

The output of the above example might look like: "Current hour: 15".

## Conclusion

Formatting time is a common task in programming, and the `std::chrono` library provides a flexible and efficient way to achieve this in C++. In this blog post, we explored how to format time as a string using `std::put_time` and how to extract individual time components using `std::tm`. By using these tools, you can accurately and easily handle time-related operations in your C++ programs.

# References:
- [std::chrono - C++ Standard Library](https://en.cppreference.com/w/cpp/chrono)
- [std::put_time - C++ Standard Library](https://en.cppreference.com/w/cpp/io/manip/put_time)