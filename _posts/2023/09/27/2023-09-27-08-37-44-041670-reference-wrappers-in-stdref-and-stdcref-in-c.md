---
layout: post
title: "Reference wrappers in std::ref and std::cref in C++"
description: " "
date: 2023-09-27
tags: [References, CPlusPlus]
comments: true
share: true
---

In C++, references are powerful tools for working with variables indirectly. However, sometimes we need to pass references to functions that do not support direct reference passing, such as `std::thread`, `std::bind`, or function objects.

To address this, the C++ standard library provides two utility functions: `std::ref` and `std::cref`, which allow us to create **reference wrappers**. These reference wrappers can then be passed to functions that expect copyable or constant copyable objects.

## std::ref

The `std::ref` function template, defined in the `<functional>` header, creates a reference wrapper for a given object. It takes any lvalue as input and returns a reference wrapper object that can be used in place of the original object.

```cpp
#include <functional>
#include <iostream>

void foo(int& val) {
    val += 5;
}

int main() {
    int num = 10;
    std::ref(num); // Reference wrapper created for 'num'

    std::thread t(foo, std::ref(num)); // Pass the reference wrapper to a thread

    t.join();
    std::cout << "Modified value: " << num << std::endl;
    return 0;
}
```

In the above example, we have a function `foo` that takes an `int&` argument. However, when we pass `num` directly to `std::thread`, it would result in a compilation error. By using `std::ref(num)` as the argument, we create a reference wrapper that can be safely passed to the thread constructor.

## std::cref

While `std::ref` is used for creating reference wrappers for non-constant objects, `std::cref` is used for creating reference wrappers for constant objects. It is also defined in the `<functional>` header.

```cpp
#include <functional>
#include <iostream>

void print(const std::string& str) {
    std::cout << "String: " << str << std::endl;
}

int main() {
    std::string message = "Hello, World!";
    
    std::thread t(print, std::cref(message)); // Pass the constant reference wrapper to a thread

    t.join();
    return 0;
}
```

In this example, the function `print` takes `const std::string&` as the argument. When passing `message` to `std::thread`, we create a constant reference wrapper using `std::cref(message)`.

## Wrapping Up

The `std::ref` and `std::cref` functions in C++ provide a convenient way to pass references to functions that do not support direct reference passing. By creating reference wrappers, we can ensure correct handling of references in scenarios where copies are not desired or supported.

So next time you encounter a situation where you need to pass references to such functions or function objects, remember to use `std::ref` for non-constant objects and `std::cref` for constant objects.

#C++ #References #CPlusPlus