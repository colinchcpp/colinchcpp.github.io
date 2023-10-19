---
layout: post
title: "Checking if a year is a leap year with std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

Determining if a year is a leap year is a common task in programming. In C++, you can use the `std::chrono::year` class from the C++ Standard Library to simplify this check. Here's an example of how to accomplish this:

```cpp
#include <iostream>
#include <chrono>

bool isLeapYear(int year) {
    std::chrono::year y{ year };
    return y.is_leap();
}

int main() {
    int year;
    std::cout << "Enter a year: ";
    std::cin >> year;

    if (isLeapYear(year)) {
        std::cout << year << " is a leap year." << std::endl;
    } else {
        std::cout << year << " is not a leap year." << std::endl;
    }

    return 0;
}
```

In this example, we define a function `isLeapYear` that takes an `int` parameter representing the year to check. Inside the function, we create a `std::chrono::year` object using the input year. Then, we use the `is_leap()` member function to determine if the year is a leap year. The function returns `true` if it is a leap year and `false` otherwise.

In the `main` function, we prompt the user to enter a year, read it from the standard input, and call the `isLeapYear` function. Based on the return value, we display whether the year is a leap year or not.

Now you can easily check if a year is a leap year using the C++ Standard Library and `std::chrono::year` class!