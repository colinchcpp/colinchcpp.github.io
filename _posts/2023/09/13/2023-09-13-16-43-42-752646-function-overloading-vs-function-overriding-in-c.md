---
layout: post
title: "Function overloading vs function overriding in C++"
description: " "
date: 2023-09-13
tags: [include, include, Programming]
comments: true
share: true
---

When working with object-oriented programming in C++, you may come across two important concepts: **function overloading** and **function overriding**. While they may sound similar, they serve different purposes in the context of C++ programming. In this blog post, we will explore the differences between function overloading and function overriding and understand when to use each technique.

## Function Overloading

Function overloading refers to the ability to define multiple functions with the same name but different parameters or types. The compiler differentiates between these functions based on their parameter lists. By overloading functions, you can have several methods with the same name but different functionalities.

Here's an example that demonstrates function overloading:

```cpp
#include <iostream>

void print(int number) {
   std::cout << "Printing integer: " << number << std::endl;
}

void print(double number) {
   std::cout << "Printing double: " << number << std::endl;
}

int main() {
   print(10);     // Calls the first overload: print(int number)
   print(3.14);   // Calls the second overload: print(double number)
   
   return 0;
}
```

In the above code, we have two `print` functions. One takes an `int` parameter, and the other takes a `double` parameter. Depending on the argument passed, the appropriate `print` function is called. This is an example of function overloading.

## Function Overriding

On the other hand, function overriding is used when you have a base class and a derived class, and you want to provide a different implementation for a specific function in the derived class. In function overriding, both the base class and the derived class have the same function signature (name and parameters).

Consider the following example:

```cpp
#include <iostream>

class Animal {
public:
   virtual void makeSound() {
      std::cout << "Animal makes a sound" << std::endl;
   }
};

class Dog : public Animal {
public:
   void makeSound() override {
      std::cout << "Dog barks" << std::endl;
   }
};

int main() {
   Animal* animal = new Dog();
   animal->makeSound();   // Calls the derived class function: Dog::makeSound()
   
   delete animal;
   return 0;
}
```

In the above code, we have a base class `Animal` and a derived class `Dog`. Both classes have a function named `makeSound`. By using the `virtual` keyword in the base class and the `override` keyword in the derived class, we explicitly indicate that the `makeSound` function should be overridden.

When we create an instance of `Dog` and call the `makeSound` function on it, the derived class's implementation is invoked instead of the base class's implementation. This is an example of function overriding.

## Conclusion

In summary, function overloading allows you to define multiple functions with the same name but different parameters or types, while function overriding enables you to provide a different implementation for a function in a derived class. Understanding the difference between function overloading and function overriding will help you design more flexible and efficient C++ programs.

#C++ #Programming