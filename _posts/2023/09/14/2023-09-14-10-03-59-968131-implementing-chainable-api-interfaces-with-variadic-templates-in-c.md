---
layout: post
title: "Implementing chainable API interfaces with variadic templates in C++"
description: " "
date: 2023-09-14
tags: [developer, cplusplus]
comments: true
share: true
---

In modern C++ programming, it is common to use fluent or chainable interfaces in APIs to achieve code that is readable, expressive, and easy to use. In this blog post, we'll explore how to implement such an interface using variadic templates in C++. 

## What is a Chainable API Interface?

A chainable API interface allows the user to call multiple functions on an object in a sequence, making the code more readable. Each function call returns a reference to the object itself, enabling fluent syntax. Let's take a simple example of a class called `Builder` that builds a string using a series of method calls:

```cpp
class Builder {
private:
    std::string result;

public:
    Builder& add(const std::string& str) {
        result += str;
        return *this;
    }

    Builder& uppercase() {
        // Convert the result to uppercase
        // ...

        return *this;
    }

    Builder& lowercase() {
        // Convert the result to lowercase
        // ...

        return *this;
    }

    std::string build() {
        return result;
    }
};
```

With this class, we can chain multiple method calls to build a string in a concise and readable way:

```cpp
Builder builder;

std::string result = builder.add("Hello ").uppercase().add("World!").build();
```

## Implementing Chainable Interfaces with Variadic Templates

While the above example works well for a small number of methods, it can become cumbersome if we have many methods. Instead, we can leverage variadic templates to create a more flexible and scalable solution.

```cpp
class Builder {
private:
    std::string result;

public:
    Builder& add(const std::string& str) {
        result += str;
        return *this;
    }

    template<typename Func, typename... Args>
    Builder& modify(Func func, const Args&... args) {
        func(result, args...);
        return *this;
    }

    std::string build() {
        return result;
    }
};
```

The `modify` method takes a function pointer or lambda and a variable number of arguments. It applies the given function to the result string along with the provided arguments.

With this approach, we can now define additional modifying functions without modifying the `Builder` class:

```cpp
void uppercase(std::string& str) {
    // Convert the str to uppercase
    // ...
}

void lowercase(std::string& str) {
    // Convert the str to lowercase
    // ...
}
```

Using the new `modify` method, we can modify the result string using the above functions:

```cpp
Builder builder;

std::string result = builder.add("Hello ").modify(uppercase).add("World!").build();
```

The `modify` method can be called multiple times with different functions:

```cpp
std::string result = builder.add("Hello ").modify(uppercase).modify(lowercase).add("World!").build();
```

## Conclusion

By leveraging variadic templates, we can create chainable API interfaces that provide a flexible and extensible way to manipulate objects. This approach allows for clean and readable code, making it easier to express complex operations in a concise manner.

Implementing chainable API interfaces with variadic templates unlocks the full potential of fluent programming in C++. So, next time you are designing an API, consider using this technique to improve the usability and readability of your code.

#developer #cplusplus