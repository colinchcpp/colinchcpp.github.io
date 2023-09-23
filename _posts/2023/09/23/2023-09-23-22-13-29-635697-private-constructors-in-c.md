---
layout: post
title: "Private Constructors in C++"
description: " "
date: 2023-09-23
tags: [constructors]
comments: true
share: true
---

In object-oriented programming, constructors are special methods used to initialize objects of a class. By default, constructors are public, allowing objects to be created from anywhere in the program. However, there are cases where you might want to restrict the creation of objects from outside the class itself. One way to achieve this is by using private constructors.

## What is a private constructor?

A private constructor is a special constructor that can only be accessed within the class in which it is defined. It cannot be invoked from outside the class or by any other class. This effectively makes the class non-creatable by external entities.

## Why use private constructors?

There are several reasons why you might want to use private constructors in your C++ code:

1. **Singleton design pattern**: A singleton is a class that allows only one instance to be created throughout the program's execution. By making the constructor private, you enforce the use of a static method to access the instance, ensuring that there is only one instance available.

2. **Utility classes**: Sometimes, you want to group related functions or provide common functionality without allowing objects to be instantiated. By making the constructor private, you prevent accidental instantiation of the class.

3. **Static classes**: A static class is a class that only contains static members and is not meant to be instantiated. By making the constructor private, you emphasize the intent of the class and prevent accidental creation of objects.

## Example usage

```cpp
class Singleton {
private:
    // Private constructor
    Singleton() {
        // Initialization code
    }

public:
    // Static method to access the instance
    static Singleton& getInstance() {
        static Singleton instance;
        return instance;
    }

    // Other class methods
    void doSomething() {
        // Code here
    }
};

int main() {
    // This will not compile - private constructor
    // Singleton myObject;

    // Access the instance through the static method
    Singleton& instance = Singleton::getInstance();

    // Call methods on the singleton object
    instance.doSomething();

    return 0;
}
```

In the example above, the Singleton class has a private constructor that cannot be accessed from outside the class. Instead, we provide a static method `getInstance()` which returns the single instance of the class, allowing controlled access to the object.

Using a private constructor in this way ensures that only one instance of the Singleton class exists in the program.

## Conclusion

Private constructors in C++ provide a mechanism for controlling object creation within a class. They are useful in scenarios where you want to restrict object creation to specific methods or prevent instantiation altogether. By using private constructors, you can enforce design patterns like the singleton pattern or create utility classes that cannot be instantiated.

#cpp #constructors