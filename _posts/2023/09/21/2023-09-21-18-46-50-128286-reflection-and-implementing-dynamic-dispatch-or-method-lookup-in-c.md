---
layout: post
title: "Reflection and implementing dynamic dispatch or method lookup in C++."
description: " "
date: 2023-09-21
tags: [include]
comments: true
share: true
---

In object-oriented programming, *dynamic dispatch* refers to the ability of a program to select the appropriate function to execute based on the actual type of an object at runtime. This is especially useful when working with polymorphic objects, where different classes may have different implementations of the same function.

C++ supports dynamic dispatch via *virtual functions*, but sometimes you may need more fine-grained control over method lookup and dispatch. In such cases, you can resort to *reflection* techniques to implement your own dynamic dispatch mechanism.

## Reflection in C++

Reflection is a mechanism that enables a program to examine and modify its own structure during runtime. C++ does not have built-in support for reflection like some other languages, such as Java or C#. However, you can use certain techniques to achieve similar functionality.

One common approach is to use a combination of templates and function pointers. Here's a simple example:

```cpp
#include <iostream>

// Base class with a virtual function
class Base {
public:
    virtual void print() { std::cout << "Base" << std::endl; }
};

// Derived class with overridden print() function
class Derived : public Base {
public:
    void print() override { std::cout << "Derived" << std::endl; }
};

// Function that performs dynamic dispatch
void dynamicDispatch(Base* obj) {
    // Use function pointers to invoke the appropriate method
    void (Base::*printFn)() = &Base::print;
    (obj->*printFn)();
}

int main() {
    Base* obj1 = new Base();
    Base* obj2 = new Derived();

    dynamicDispatch(obj1);  // Output: Base
    dynamicDispatch(obj2);  // Output: Derived

    delete obj1;
    delete obj2;

    return 0;
}
```

In this example, we have a `Base` class with a virtual `print()` function. The `Derived` class overrides this function. The `dynamicDispatch()` function takes a `Base` pointer and uses function pointers to invoke the appropriate method based on the actual type of the object.

## Implementing Method Lookup

To implement a more complex method lookup mechanism, you can use techniques like *method tables* or *dictionaries*. A method table is an array of function pointers, where each element corresponds to a specific method. By indexing the table based on a method identifier or name, you can dynamically dispatch the appropriate method.

Here's a simplified example using a method table:

```cpp
#include <iostream>
#include <functional>
#include <unordered_map>

// Base class with virtual functions
class Base {
public:
    virtual void method1() { std::cout << "Base::method1" << std::endl; }
    virtual void method2() { std::cout << "Base::method2" << std::endl; }
};

// Derived class with overridden methods
class Derived : public Base {
public:
    void method1() override { std::cout << "Derived::method1" << std::endl; }
    void method2() override { std::cout << "Derived::method2" << std::endl; }
};

// Method table type
using MethodTable = std::unordered_map<std::string, std::function<void(Base*)>>;

// Function that performs method lookup and dispatch
void dynamicDispatch(Base* obj, const MethodTable& methodTable, const std::string& methodName) {
    auto it = methodTable.find(methodName);
    if (it != methodTable.end())
        it->second(obj);
    else
        std::cerr << "Method not found: " << methodName << std::endl;
}

int main() {
    Base* obj1 = new Base();
    Base* obj2 = new Derived();

    // Initialize method table
    MethodTable methodTable = {
        { "method1", [](Base* obj) { obj->method1(); } },
        { "method2", [](Base* obj) { obj->method2(); } }
    };

    dynamicDispatch(obj1, methodTable, "method1");  // Output: Base::method1
    dynamicDispatch(obj2, methodTable, "method2");  // Output: Derived::method2

    delete obj1;
    delete obj2;

    return 0;
}
```

In this example, we define a `Base` class with two virtual functions, `method1()` and `method2()`. The `Derived` class overrides these functions. The `dynamicDispatch()` function performs the method lookup and dispatch by searching for the method name in the provided method table and invoking the corresponding function using a lambda expression.

By using method lookup mechanisms like this, you can achieve dynamic dispatch and customize the behavior of your program based on the runtime types of objects.

## Conclusion

Dynamic dispatch is a powerful concept in object-oriented programming, allowing programs to select the appropriate function to execute based on the actual type of an object at runtime. While C++ provides support for dynamic dispatch via virtual functions, you can implement your own mechanism using reflection techniques. By leveraging templates, function pointers, and method lookup mechanisms, you can achieve more fine-grained control over dynamic dispatch in your C++ programs.