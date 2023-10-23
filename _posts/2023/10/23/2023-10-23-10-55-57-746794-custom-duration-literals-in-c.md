---
layout: post
title: "Custom duration literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---
In this blog post, we will explore how to create custom duration literals in C++. Duration literals provide a convenient way to express time durations in code. By default, the C++ standard library provides literals for common time units like seconds, minutes, and hours. However, sometimes you may need to work with custom time units that are not natively supported. In such cases, custom duration literals come to the rescue.

## What are Duration Literals?
Duration literals are a way to represent a time interval in a concise and readable way. They allow you to express time durations in code without explicitly specifying the unit of time. For example, instead of writing `60 * 1000`, you can write `1s` to represent a duration of 1 second. This improves the readability of your code and makes it more expressive.

## Creating Custom Duration Literals
To create custom duration literals, you need to define a user-defined literal operator. This operator is responsible for converting the literal into the desired duration type. Here's an example of how to define a custom duration literal for milliseconds:

```cpp
#include <chrono>

constexpr std::chrono::milliseconds operator"" _ms(unsigned long long milliseconds) {
    return std::chrono::milliseconds(milliseconds);
}
```

In this example, we define a user-defined literal operator `operator"" _ms`. It takes an unsigned long long parameter representing the duration in milliseconds. The operator body simply constructs and returns a `std::chrono::milliseconds` object with the provided value.

## Using Custom Duration Literals
Once you have defined the custom duration literal, you can easily use it in your code. Here's an example of how to use the `_ms` literal:

```cpp
#include <iostream>

int main() {
    using namespace std::chrono_literals;

    auto duration = 500_ms;

    std::cout << "Duration: " << duration.count() << " milliseconds\n";
    
    return 0;
}
```

In this example, we include the `chrono_literals` namespace to enable the use of all standard duration literals. We then use the `_ms` literal to create a duration of 500 milliseconds. Finally, we print the count of the duration in milliseconds.

## Conclusion
Custom duration literals in C++ provide a powerful way to express time durations in a concise and expressive manner. By defining your own literals, you can work with custom time units seamlessly. This allows you to write more readable and maintainable code. So go ahead and try creating your own custom duration literals in your C++ projects!

## References
- [C++ reference - Duration literals](https://en.cppreference.com/w/cpp/chrono/duration_literal)
- [Bjarne Stroustrup's C++11 FAQ - User-Defined Literals](http://www.stroustrup.com/C++11FAQ.html#UD-literals)