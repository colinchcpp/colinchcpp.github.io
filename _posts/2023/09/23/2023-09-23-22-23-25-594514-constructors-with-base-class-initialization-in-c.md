---
layout: post
title: "Constructors with Base Class Initialization in C++"
description: " "
date: 2023-09-23
tags: [include, inheritance]
comments: true
share: true
---

When working with inheritance in C++, it is common to have a derived class that inherits from a base class. In such scenarios, it is important to properly initialize the base class members in the derived class's constructor.

To initialize base class members from the derived class constructor, you can use the constructor initializer list. The constructor initializer list allows you to call the base class constructor and pass any required arguments.

Here's an example to illustrate how to initialize base class members in a derived class constructor:

```cpp
#include <iostream>

class Base {
public:
    Base(int value) : baseValue(value) {
        std::cout << "Base class constructor called." << std::endl;
    }
    
    void printValue() const {
        std::cout << "Base class value: " << baseValue << std::endl;
    }
    
protected:
    int baseValue;
};

class Derived : public Base {
public:
    Derived(int baseValue, int derivedValue)
        : Base(baseValue), derivedValue(derivedValue) {
        std::cout << "Derived class constructor called." << std::endl;
    }
    
    void printValues() const {
        std::cout << "Base class value: " << baseValue << std::endl;
        std::cout << "Derived class value: " << derivedValue << std::endl;
    }
    
private:
    int derivedValue;
};

int main() {
    Derived derivedObj(10, 20);
    derivedObj.printValues();
    
    return 0;
}
```

In the above example, we have a base class `Base` that takes an integer argument in its constructor. The derived class `Derived` inherits from `Base` and also has an additional member variable.

To properly initialize the base class member `baseValue` in the derived class constructor, we use the constructor initializer list `: Base(baseValue)` before initializing the derived class member `derivedValue`.

Running the above code will output the following:

```
Base class constructor called.
Derived class constructor called.
Base class value: 10
Derived class value: 20
```

As you can see, the base class constructor is called first, followed by the derived class constructor. The base class member `baseValue` is properly initialized using the passed argument, and both base and derived class values are printed correctly.

Using constructor initializer lists to initialize base class members in derived class constructors ensures proper initialization and avoids potential issues in the inheritance hierarchy.

#cpp #inheritance