---
layout: post
title: "Constructor in Destructor in C++"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

The syntax for defining a destructor in C++ is similar to that of a constructor, but with a `~` symbol followed by the class name. Here's an example:

```cpp
class MyClass {
public:
    // Constructor
    MyClass() {
        std::cout << "Constructor called" << std::endl;
    }

    // Destructor
    ~MyClass() {
        std::cout << "Destructor called" << std::endl;
    }
};

int main() {
    MyClass obj1; // Constructor called

    // Block scope
    {
        MyClass obj2; // Constructor called
    } // Destructor called (obj2 goes out of scope)

    // Destructor called (obj1 goes out of scope)

    return 0;
}
```

In the above example, when an object of the `MyClass` is created using `MyClass obj1`, the constructor is called and it prints "Constructor called" to the console. Similarly, when the `obj1` and `obj2` objects go out of scope, their destructors are called and they print "Destructor called".

The destructor is automatically called by the compiler at the appropriate time, and you do not need to explicitly call it. However, it is good practice to define a destructor if your class manages any resources, especially if they need to be properly cleaned up before the object is destroyed.

Note that the order of destruction for objects is the reverse of their order of construction. In the above example, `obj2` is destroyed before `obj1`.