---
layout: post
title: "References to temporaries in C++"
description: " "
date: 2023-09-27
tags: [temporaries]
comments: true
share: true
---

In C++, a temporary is an object that is created by the compiler during expression evaluation. It is often used when returning a value from a function or during complex expressions involving temporary objects. One important aspect to consider when working with temporaries is how references behave.

When a temporary object is created, it can be bound to a reference, extending its lifetime. However, there are a few rules and considerations to keep in mind when working with references to temporaries:

## Binding Temporary to a Reference

A temporary object can be bound to a reference if the reference type is compatible with the object's type. This is typically done using a const reference, as it ensures that the object cannot be modified through the reference. Here's an example:

```cpp
const int& ref = 42;
```

In this case, the temporary object `42` is bound to the `const int&` reference `ref`. The lifetime of `ref` is extended to match the lifetime of the temporary object.

## Restrictions on Modifying References to Temporaries

When binding a temporary object to a reference, it is important to note that modifying the reference is not allowed. Only `const` references can be bound to temporaries. For example:

```cpp
int& ref = 42;  // ERROR: Cannot bind non-const lvalue reference to a temporary object
```

Attempting to bind a non-const lvalue reference to a temporary object will result in a compilation error.

## Lifetime Extension

The lifetime of a temporary object bound to a reference is extended to match the lifetime of the reference. This means that the temporary object will live as long as the reference is in scope. It is crucial to ensure that the reference is still valid and in scope when accessing the temporary object.

## Considerations when Returning References

Returning a reference to a local object is generally considered bad practice in C++. This is because the local object's lifetime ends when the function returns, leading to a dangling reference. However, returning a temporary object by value or by const reference is completely safe.

```cpp
const std::string& getGreeting() {
    return "Hello, World!";  // Safe: Temporary object lifetime is extended
}
```

In this example, the function returns a temporary string object by const reference. The lifetime of the temporary object is extended until the reference is no longer in scope.

## Conclusion

Working with references to temporaries in C++ requires careful consideration. By understanding the rules and limitations surrounding the binding and lifetime of temporary objects, you can safely use references to enhance code readability and performance in certain scenarios.

#temporaries #C++