---
layout: post
title: "Common mistakes to avoid when using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: [uniform]
comments: true
share: true
---

Uniform Initialization is a feature introduced in C++11 that provides a unified way to initialize variables, objects, and containers. While it offers a cleaner and more intuitive syntax, there are some common mistakes that developers may encounter when using uniform initialization. In this blog post, we will discuss some of these mistakes and how to avoid them.

## Table of Contents
- [Misusing parentheses](#misusing-parentheses)
- [Unexpected narrowing conversions](#unexpected-narrowing-conversions)
- [Forgetting about aggregate initialization](#forgetting-about-aggregate-initialization)
- [Conclusion](#conclusion)

## Misusing parentheses

One common mistake with uniform initialization is misplacing parentheses. In uniform initialization, parentheses are used to initialize objects or call constructors, but using them incorrectly can lead to unexpected behavior. Let's look at an example:

```cpp
int x(5);    // correctly initializes x to 5
int y{5};    // also correctly initializes y to 5
int z(5.5);  // mistakenly initializes z to 5, narrowing conversion occurs
int w{5.5};  // error! narrowing conversion from double to int
```

In the above code, using parentheses to initialize `z` results in a narrowing conversion, where the value 5.5 is truncated to an integer value of 5. On the other hand, using braces correctly triggers a compilation error when a narrowing conversion is detected, preventing potential bugs.

To avoid this mistake, always use braces `{}` for initialization when possible. This helps ensure that the compiler catches narrowing conversions and avoids unintended behavior.

## Unexpected narrowing conversions

As mentioned earlier, narrowing conversions can occur when using uniform initialization. A narrowing conversion is a conversion that may lose information or change the value of the initialized object. Here's an example:

```cpp
int num = {3.1415};  // error! narrowing conversion from double to int
```

In the above code, the value `3.1415` is a `double`, but we are trying to initialize an `int` variable using braces. This is considered a narrowing conversion since the `double` value will be truncated to an `int` value, resulting in a potential loss of information. To avoid this error, either use explicit type casting or choose an appropriate type for the initialization.

## Forgetting about aggregate initialization

Uniform initialization also supports aggregate initialization, which allows initializing aggregate types, such as arrays and structs, in a concise and intuitive manner. However, one common mistake is forgetting that aggregate initialization does not perform any constructor calls. Let's consider the following example:

```cpp
struct Point {
    int x;
    int y;
};

int main() {
    Point p1{1, 2};  // correctly initializes p1
    Point p2(3, 4);  // error! constructor call not supported for aggregate types
    return 0;
}
```

In the above code, using braces `{}` initializes `p1` correctly as it performs aggregate initialization. However, using parentheses `()` for initialization attempts to call a constructor, which is not supported for aggregate types. To avoid this mistake, always use braces `{}` for aggregate initialization.

## Conclusion

Uniform initialization in C++ is a powerful feature that provides a consistent and intuitive way to initialize variables, objects, and containers. However, it's important to be aware of common mistakes that can occur, such as misusing parentheses, unexpected narrowing conversions, and forgetting about aggregate initialization. By understanding these pitfalls and applying best practices, you can make the most out of uniform initialization and write cleaner and more robust code.

_[References:](https://en.cppreference.com/w/c/language/initialization)_

#cpp #uniform-initialization