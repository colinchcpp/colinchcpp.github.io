---
layout: post
title: "Extended friend declarations for more granular access control"
description: " "
date: 2023-10-13
tags: []
comments: true
share: true
---

In C++, the `friend` keyword is used to allow a class or function to access the private members of another class. This can be useful in certain situations, but it has the drawback of granting access to all private members of the class. However, with extended friend declarations, we can have more granular control over which specific members are allowed access.

To understand extended friend declarations, let's consider an example scenario. Suppose we have a class called `A` with private member variables `x` and `y`, and we want to grant access to only the `x` member to another class called `B`. Traditionally, we would use a regular friend declaration to grant access to `B` for all private members of `A`. However, using extended friend declarations, we can limit the access to just the `x` member.

Here's how extended friend declarations can be used:

```cpp
class A {
    int x;
    int y;

    friend class B;
    friend int B::getX();
};

class B {
    int z;

public:
    int getX() {
        A objA;
        return objA.x; // Accessible as `x` is a friend of `B`
    }
};
```

In the example above, by using the extended friend declaration `friend int B::getX();` inside class `A`, we specify that only the `getX()` member of class `B` is allowed access to the private members of `A`. This means that `B` can access `x`, but not `y` or any other private members of `A`.

This approach provides more control over access control, helping to enforce encapsulation and maintain code integrity. Granular access control allows us to define specific relationships between classes without exposing more than necessary.

It's important to note that extended friend declarations are only available in C++ and cannot be used in other programming languages.

In conclusion, extended friend declarations in C++ offer a more fine-grained approach to control access to private members of a class. By using extended friend declarations, we can limit access to specific members, ensuring better encapsulation and code organization.