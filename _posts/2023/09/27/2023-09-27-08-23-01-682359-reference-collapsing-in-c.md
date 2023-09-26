---
layout: post
title: "Reference collapsing in C++"
description: " "
date: 2023-09-27
tags: [ReferenceCollapsing]
comments: true
share: true
---

In C++, reference collapsing is a rule that determines the resulting type when references are combined together. It is a fundamental concept to understand when working with references in templates and type deduction.

## The Rule of Reference Collapsing

The rule of reference collapsing states that when two references are combined, the resulting type depends on the combination of the references involved. Here are the possible combinations:

1. When one or both references are rvalue references (`&&`), the result is an rvalue reference.

2. When one of the references is an lvalue reference (`&`), and the other is an rvalue reference, the result is an lvalue reference.

3. When both references are lvalue references, the result is an lvalue reference.

## Example Code

Let's take a look at some example code to better understand how reference collapsing works:

```cpp
template <typename T>
void foo(T&& arg) {
    T& lref = arg;
    T&& rref = arg;
}

int main() {
    int value = 42;
    foo(value); // arg will have type int&
    foo(123);   // arg will have type int&&
    
    return 0;
}
```

In the `foo` function, `T&&` is a forwarding reference (also known as universal reference) because `T` is a template parameter. Inside `foo`, we can create both an lvalue reference (`lref`) and an rvalue reference (`rref`) to `arg`.

When calling `foo` with `value` as an argument, the type of `arg` will be `int&`, following the reference collapsing rule. Similarly, when calling `foo` with `123`, the type of `arg` will collapse to `int&&`.

## Conclusion

Understanding reference collapsing in C++ is essential when working with templates and type deduction. By applying the rule of reference collapsing, you can determine the resulting type when combining references. This knowledge is particularly useful when dealing with forward references or writing generic code.

#Cpp #ReferenceCollapsing