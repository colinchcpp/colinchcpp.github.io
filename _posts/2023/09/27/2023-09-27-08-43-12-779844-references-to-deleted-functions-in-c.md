---
layout: post
title: "References to deleted functions in C++"
description: " "
date: 2023-09-27
tags: [DeletedFunctions]
comments: true
share: true
---

In C++, a deleted function is a member function that has been explicitly marked as deleted using the `delete` keyword. The purpose of a deleted function is to prevent its usage, either to enforce certain design constraints or to avoid ambiguous or unsafe scenarios.

When a deleted function is referenced, it results in a compile-time error, indicating that the function cannot be called or used in any way. This helps in catching potential issues during the compilation process itself.

## Usage of Deleted Functions

Here's an example that illustrates the usage of deleted functions in C++:

```cpp
class NonCopyable {
public:
    NonCopyable() = default;
    NonCopyable(const NonCopyable&) = delete;             // Delete copy constructor
    NonCopyable& operator=(const NonCopyable&) = delete;  // Delete copy assignment operator

    // Other member functions...
};

int main() {
    NonCopyable obj1;
    NonCopyable obj2(obj1);             // Error: attempting to copy construct obj2 from obj1
    NonCopyable obj3;
    obj3 = obj1;                        // Error: attempting to copy assign obj1 to obj3

    return 0;
}
```

In the above example, the class `NonCopyable` contains deleted copy constructor and copy assignment operator. By doing so, we explicitly prevent the creation of new objects through copying.

Attempting to copy construct `obj2` from `obj1` or copy assign `obj1` to `obj3` will result in compile-time errors. This helps in enforcing the intention of not allowing copying of objects of `NonCopyable` class.

## Benefits and Use Cases

Deleted functions provide several benefits in C++ programming:

- **Preventing unwanted operations**: By deleting certain functions, we can restrict the usage of those functions, helping to prevent misuse and unintended behavior.
- **Enforcing design constraints**: Deleted functions can enforce specific design choices, such as disallowing object copying or preventing certain operations on specific instances.
- **Avoiding ambiguity**: In certain cases, the presence of a deleted function can help avoid ambiguous scenarios where multiple overloaded functions could potentially match the given arguments.

To conclude, deleted functions in C++ are useful tools for enforcing design constraints, preventing unwanted operations, and improving code clarity. Correctly using deleted functions in your codebase can help catch errors at compile-time and facilitate better software development practices.

#Cpp #DeletedFunctions