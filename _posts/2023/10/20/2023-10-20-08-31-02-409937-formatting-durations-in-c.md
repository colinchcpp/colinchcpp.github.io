---
layout: post
title: "Formatting durations in C++"
description: " "
date: 2023-10-20
tags: [References, cplusplus]
comments: true
share: true
---

## Introduction
When working with durations in C++, it is often required to format them in a human-readable manner. In this article, we will explore different ways to format durations and convert them into a string representation using the C++ programming language.

## Using std::chrono
C++11 introduced the `<chrono>` library, which provides a comprehensive set of facilities for working with time. The `std::chrono::duration` class represents a duration in terms of a count of ticks, where each tick represents a specified unit of time.

To format a duration, we can use the `std::chrono::duration_cast` function to convert it into a desired unit of time, such as hours, minutes, and seconds. We can then extract the individual components and format them as needed.

Here's an example:

```cpp
#include <iostream>
#include <chrono>
#include <string>

std::string formatDuration(std::chrono::milliseconds duration) {
    using namespace std::chrono;

    auto hours = duration_cast<hours>(duration);
    duration -= hours;
    auto minutes = duration_cast<minutes>(duration);
    duration -= minutes;
    auto seconds = duration_cast<seconds>(duration);
    duration -= seconds;
    auto milliseconds = duration_cast<milliseconds>(duration);

    std::string result;
    result += std::to_string(hours.count()) + "h ";
    result += std::to_string(minutes.count()) + "m ";
    result += std::to_string(seconds.count()) + "s ";
    result += std::to_string(milliseconds.count()) + "ms";

    return result;
}

int main() {
    std::chrono::milliseconds duration(9832074);
    std::cout << formatDuration(duration) << std::endl;

    return 0;
}
```

Output:
```
2h 43m 52s 74ms
```

In the above example, we define a `formatDuration` function that takes a `std::chrono::milliseconds` duration as an input. We then use `duration_cast` to extract hours, minutes, seconds, and milliseconds from the duration. Finally, we format these components into a string representation.

## Boost.DateTime
If you are using an older version of C++ that does not have `<chrono>` available, you can utilize the Boost C++ Libraries, specifically the `boost::posix_time` and `boost::date_time` libraries. Boost.DateTime provides similar functionality for working with durations.

Here's an example using Boost.DateTime:

```cpp
#include <iostream>
#include <boost/date_time/posix_time/posix_time.hpp>

std::string formatDuration(boost::posix_time::time_duration duration) {
    using namespace boost::posix_time;
    std::ostringstream oss;

    auto hours = duration.hours();
    auto minutes = duration.minutes();
    auto seconds = duration.seconds();
    auto milliseconds = duration.total_milliseconds() % 1000;

    oss << hours << "h " << minutes << "m " << seconds << "s " << milliseconds << "ms";
    return oss.str();
}

int main() {
    boost::posix_time::time_duration duration = boost::posix_time::milliseconds(9832074);
    std::cout << formatDuration(duration) << std::endl;

    return 0;
}
```

Output:
```
2h 43m 52s 74ms
```

In the above example, we include the Boost.DateTime library and define a `formatDuration` function that takes a `boost::posix_time::time_duration` duration as an input. We then extract hours, minutes, seconds, and milliseconds from the duration using various member functions provided by Boost.DateTime. Finally, we format these components into a string representation.

## Conclusion
Formatting durations in C++ can be done using the `<chrono>` library introduced in C++11 or the Boost.DateTime library for older versions of C++. By converting the duration into its individual components (hours, minutes, seconds, etc.) and formatting them accordingly, we can create a human-readable representation of the duration.

#References
- [`<chrono> - std::chrono`](https://en.cppreference.com/w/cpp/chrono)
- [Boost.DateTime](https://www.boost.org/doc/libs/1_77_0/doc/html/date_time.html)

#cplusplus #datetime