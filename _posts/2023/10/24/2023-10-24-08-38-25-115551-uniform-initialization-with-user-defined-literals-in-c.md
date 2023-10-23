---
layout: post
title: "Uniform initialization with user-defined literals in C++"
description: " "
date: 2023-10-24
tags: [references]
comments: true
share: true
---

Uniform initialization is a modern feature of C++ that allows initialization of variables using a consistent syntax. It introduced a more concise and consistent way to initialize variables and objects. In addition to built-in types, C++ also allows defining user-defined literals to enable developers to create custom types with their own initialization rules.

## User-Defined Literals

User-defined literals are a powerful feature in C++ that allow you to create your own literal suffixes for integer, floating-point, and string literals. This feature enables you to define custom types and specify their initialization rules.

When defining a user-defined literal, you need to specify the literal's suffix and the conversion function that will be called when the literal appears in the code.

```cpp
// Defining a user-defined literal for time durations
constexpr long long operator"" _ms(unsigned long long milliseconds)
{
    return milliseconds;
}

// Using the user-defined literal
int main()
{
    auto duration = 5000_ms; // Represents 5000 milliseconds

    // Use the duration in calculations
    int seconds = duration / 1000;
    std::cout << "Duration in seconds: " << seconds << std::endl;

    return 0;
}
```

In the above example, we define a user-defined literal `_ms` that takes an `unsigned long long` parameter representing milliseconds. The operator function converts the value to the desired representation and returns it. In the `main()` function, we can use the `_ms` literal to initialize the `duration` variable with a value of 5000 milliseconds.

## Uniform Initialization with User-Defined Literals

Uniform initialization can be combined with user-defined literals to provide a concise and expressive syntax for initializing user-defined types. By defining a constructor that takes the desired parameters, you can initialize the object using the user-defined literal syntax.

```cpp
// User-defined class with a constructor taking a duration and unit
class Duration
{
public:
    Duration(unsigned long long duration, const std::string& unit)
        : duration_(duration), unit_(unit)
    {
        // Additional initialization code if needed
    }

private:
    unsigned long long duration_;
    std::string unit_;
};

// User-defined literal for Duration
constexpr Duration operator"" _duration(unsigned long long duration)
{
    return Duration(duration, "seconds");
}

// Using the user-defined literal to create Duration objects
int main()
{
    auto duration1 = 5000_duration; // Represents a duration of 5000 seconds
    auto duration2 = 2_duration; // Represents a duration of 2 seconds

    // Use the durations as needed
    // ...

    return 0;
}
```

In the above example, we define a user-defined class `Duration`, which takes a duration value and a unit string. By defining a constructor for the `Duration` class, we can initialize objects of this class using the user-defined literal `_duration`.

In the `main()` function, we can use the `_duration` literal to initialize `duration1` and `duration2` objects, representing durations of 5000 seconds and 2 seconds, respectively.

## Conclusion

Uniform initialization in C++ provides a consistent and concise syntax for initializing variables and objects. When combined with user-defined literals, it becomes even more powerful, allowing developers to create custom types with their own initialization rules. This feature enhances code readability and expressiveness, making the code more maintainable and easier to understand.

By using user-defined literals, you can create a more natural and intuitive way to initialize your custom types, improving the overall developer experience in C++. So, make the most of uniform initialization and user-defined literals to enhance your codebase and make it more expressive.

#references:
- [C++ User-Defined Literals](https://en.cppreference.com/w/cpp/language/user_literal) 
- [C++ Uniform Initialization](https://en.cppreference.com/w/cpp/language/list_initialization)