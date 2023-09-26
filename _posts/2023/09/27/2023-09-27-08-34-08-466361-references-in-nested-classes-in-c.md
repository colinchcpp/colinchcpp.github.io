---
layout: post
title: "References in nested classes in C++"
description: " "
date: 2023-09-27
tags: [NestedClasses]
comments: true
share: true
---

To reference the outer class from within a nested class in C++, you can use the scope resolution operator (::) followed by the outer class name.

Here is an example to illustrate how to reference the outer class from within a nested class:

```cpp
#include <iostream>

class OuterClass {
private:
    int outerMember;

public:
    class NestedClass {
    public:
        void displayOuterMember(OuterClass& outer) {
            std::cout << "Outer class member: " << outer.outerMember << std::endl;
        }
    };
};

int main() {
    OuterClass outer;
    OuterClass::NestedClass nested;

    nested.displayOuterMember(outer);

    return 0;
}
```

In the above example, we have an `OuterClass` that contains a nested class `NestedClass`. Inside `NestedClass`, we define a member function `displayOuterMember` that takes an instance of the outer class as a parameter.

In the `main` function, we create an object of the outer class `OuterClass` and an object of the nested class `OuterClass::NestedClass`. We then call the `displayOuterMember` function on the `nested` object, passing the `outer` object as an argument.

Inside the `displayOuterMember` function, we use the `outer` parameter to access the `outerMember` variable of the outer class. 

By using the scope resolution operator (::), we can reference the outer class from within the nested class and access its members and methods.

Remember, when referencing the outer class from within a nested class, the outer class must be fully defined before the nested class can be used.

#C++ #NestedClasses