---
layout: post
title: "Non-const references in C++"
description: " "
date: 2023-09-27
tags: [references]
comments: true
share: true
---

When working with C++, you often come across references as a way to alias or access objects. References allow you to create an alternate name for an existing object without actually copying its data. However, there are two types of references in C++: const references and non-const references.

## Const References

A const reference is a reference that is bound to a const object. It ensures that the object it references cannot be modified through the reference. For example:

```cpp
void printData(const int& value) {
    // Cannot modify value through the const reference
    cout << value << endl;
}

int main() {
    int number = 42;
    printData(number);
    return 0;
}
```
In the code snippet above, the `printData` function takes a const reference to an integer. This means that inside the function, you cannot modify the value of the integer through the reference.

## Non-const References

On the other hand, non-const references allow you to modify the object they reference. They are denoted simply by using the `&` symbol without the `const` qualifier. Here's an example:

```cpp
void increment(int& value) {
    value++;
}

int main() {
    int counter = 0;
    increment(counter);
    cout << counter << endl;
    return 0;
}
```
In the code above, the `increment` function takes a non-const reference to an integer. This means that the value of the integer can be modified through the reference.

Non-const references are particularly useful when you want a function to modify the state of an object or when you want to pass an object by reference to avoid unnecessary copying.

It's important to remember that non-const references must be bound to modifiable objects. You cannot bind a non-const reference to a constant or temporary object.

**Summary**

Non-const references in C++ allow you to modify objects through references. They are denoted by using the `&` symbol without the `const` qualifier. Non-const references are commonly used when you want a function to modify the state of an object or when you want to avoid unnecessary copying of objects.

#cpp #references