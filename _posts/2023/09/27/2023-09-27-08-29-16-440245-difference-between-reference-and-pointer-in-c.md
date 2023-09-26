---
layout: post
title: "Difference between reference and pointer in C++"
description: " "
date: 2023-09-27
tags: [ReferenceVsPointer]
comments: true
share: true
---

In C++, references and pointers are both important concepts for manipulating and accessing data. While they may seem similar, there are significant differences between the two. In this blog post, we will explore the differences between references and pointers in C++.

## References

A reference in C++ is an alias for an existing object. It provides a way to access the object using a different name. Once initialized, a reference cannot be reassigned to refer to a different object. 

Here is an example of how to define and use a reference:

```cpp
int originalVariable = 10;
int& ref = originalVariable;

cout << "Value of originalVariable: " << originalVariable << endl;
cout << "Value of ref: " << ref << endl;

ref = 20; // Change the value of originalVariable

cout << "Value of originalVariable after change: " << originalVariable << endl;
cout << "Value of ref after change: " << ref << endl;
```

The output of the above code will be:

```
Value of originalVariable: 10
Value of ref: 10
Value of originalVariable after change: 20
Value of ref after change: 20
```

As you can see, changes made through the reference (`ref`) affect the original variable (`originalVariable`).

## Pointers

A pointer in C++ is a variable that stores the memory address of another variable. Pointers are used to manipulate memory directly and provide more flexibility than references.

Here is an example of how to define and use a pointer:

```cpp
int originalVariable = 10;
int* pointer = &originalVariable;

cout << "Value of originalVariable: " << originalVariable << endl;
cout << "Value of pointer: " << *pointer << endl;

*pointer = 20; // Change the value of originalVariable

cout << "Value of originalVariable after change: " << originalVariable << endl;
cout << "Value of pointer after change: " << *pointer << endl;
```

The output of the above code will be the same as the previous example:

```
Value of originalVariable: 10
Value of pointer: 10
Value of originalVariable after change: 20
Value of pointer after change: 20
```

As you can see, changes made via the pointer (`*pointer`) also affect the original variable (`originalVariable`).

## Differences between References and Pointers

1. **Reassignment**: Once a reference is initialized, it cannot be reassigned to refer to a different object. On the other hand, pointers can be re-assigned to point to different objects.
2. **Nullability**: References cannot be null, and they must always refer to a valid object. Pointers, on the other hand, can be assigned a null value that indicates they are not pointing to any valid memory address.
3. **Syntax**: References are defined using the `&` symbol, whereas pointers are defined using the `*` symbol. 

In summary, references and pointers are both useful in C++, but they have different behaviors and use cases. References provide an alternative name for an object and are useful when you want to avoid modifying the original variable. Pointers, on the other hand, allow you to directly manipulate memory and are more flexible in terms of reassignment. Understanding the differences between the two is crucial for writing efficient and correct C++ code.

#C++ #ReferenceVsPointer