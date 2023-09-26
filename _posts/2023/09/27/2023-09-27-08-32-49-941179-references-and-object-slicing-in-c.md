---
layout: post
title: "References and object slicing in C++"
description: " "
date: 2023-09-27
tags: [references, objectslicing]
comments: true
share: true
---

When working with objects in C++, it is important to understand the concepts of **references** and **object slicing**. These concepts play a significant role in the behavior of objects and can sometimes lead to unexpected results if not understood properly.

## References in C++

A **reference** in C++ is an alias or alternative name for an existing object. It provides an alternate way to access and modify the object without changing the object itself. References are often used as function parameters to avoid making unnecessary copies of objects.

Consider the following example:

```cpp
#include <iostream>

void increment(int& num) {
    num++;
}

int main() {
    int number = 5;
    int& refNumber = number;

    std::cout << "Original number: " << number << std::endl; // Output: Original number: 5

    increment(refNumber);
    
    std::cout << "Modified number: " << number << std::endl; // Output: Modified number: 6
    
    return 0;
}
```

In this example, the `increment` function takes a reference to an `int` variable `num` as a parameter. By passing `refNumber` as an argument to this function, we can modify the original `number` variable directly within the function, and the change will be reflected in the `main` function.

## Object Slicing in C++

**Object slicing** occurs when a derived class object is assigned to a base class object, resulting in the loss of derived class specific information. This happens because the base class object can only store the base class attributes and methods.

Let's consider the following example:

```cpp
#include <iostream>

class Animal {
protected:
    std::string name;

public:
    Animal(const std::string& name) : name(name) {}
    
    virtual std::string getSound() const {
        return "Unknown sound";
    }
};

class Dog : public Animal {
public:
    Dog(const std::string& name) : Animal(name) {}
    
    std::string getSound() const override {
        return "Bark";
    }
};

int main() {
    Dog dog("Buddy");
    Animal animal = dog; // Object slicing

    std::cout << "Dog sound: " << dog.getSound() << std::endl; // Output: Dog sound: Bark
    std::cout << "Animal sound: " << animal.getSound() << std::endl; // Output: Animal sound: Unknown sound
    
    return 0;
}
```

In this example, we have a base class `Animal` and a derived class `Dog`. The `Dog` class overrides the `getSound()` method. However, when we assign a `Dog` object to an `Animal` object, the derived class-specific information is sliced off, and we lose the ability to access the `getSound()` method specific to the `Dog` class.

To avoid object slicing and preserve the derived class information, it's common to use **pointers** or **references** to objects instead of assigning them directly.

Understanding references and object slicing is essential in C++ programming. Properly utilizing references can make your code more efficient, while being aware of object slicing can help you avoid unexpected behavior. #references #objectslicing