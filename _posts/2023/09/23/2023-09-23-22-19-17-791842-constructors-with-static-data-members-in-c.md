---
layout: post
title: "Constructors with Static Data Members in C++"
description: " "
date: 2023-09-23
tags: [include]
comments: true
share: true
---

In C++, static data members are shared among all the instances of a class. They belong to the class itself rather than individual objects. Constructors with static data members can be used to initialize these shared variables.

By using constructors with static data members, you can ensure that the shared variables are properly initialized before any object of the class is created.

## Example

```cpp
#include <iostream>

class MyClass {
private:
    static int count; // static data member

public:
    MyClass() {
        count++; // increment count on object creation
    }

    static void printCount() {
        std::cout << "Count: " << count << std::endl;
    }
};

int MyClass::count = 0; // initializing the static data member

int main() {
    MyClass obj1;
    MyClass obj2;
    MyClass obj3;

    MyClass::printCount(); // Output: Count: 3

    return 0;
}
```

In the above example, `count` is a static data member of the `MyClass` class. It is initialized to 0 outside of the class. 

The constructor `MyClass()` increments the `count` variable every time an object of the class is created. 

The `printCount()` function is a static member function that prints the value of `count`.

In the `main()` function, three objects of `MyClass` are created, and the `printCount()` function is called to display the count.

By using constructors with static data members, you can keep track of the number of objects created from a particular class.

## Conclusion

Constructors with static data members in C++ are useful when you want to initialize and use shared variables among all instances of a class. They provide a way to ensure consistent initialization and management of these variables.