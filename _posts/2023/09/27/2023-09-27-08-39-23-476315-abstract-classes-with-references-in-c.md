---
layout: post
title: "Abstract classes with references in C++"
description: " "
date: 2023-09-27
tags: [AbstractClasses, References]
comments: true
share: true
---

In object-oriented programming, an abstract class serves as a blueprint for other classes and cannot be instantiated itself. It may contain pure virtual functions, which are essentially placeholders for functions that must be implemented by any derived class.

In C++, we can use references to abstract classes to achieve polymorphism and provide flexibility in the design of our code. Let's explore how to use abstract classes with references in C++.

## Declaring an Abstract Class
To declare an abstract class, we use the `virtual` keyword for any member functions that we want to be pure virtual. Here's an example:

```cpp
class Animal {
public:
    virtual void makeSound() = 0; // pure virtual function
};
```

In the above code, the `Animal` class is declared as an abstract class because it contains a pure virtual function `makeSound()`. Any derived class must implement this function.

## Using References to Abstract Classes
We can create references to abstract classes in order to achieve polymorphism. This allows us to use objects of any derived class through the abstract class reference.

Let's create two derived classes `Cat` and `Dog` that inherit from the `Animal` abstract class and implement the `makeSound()` function:

```cpp
class Cat : public Animal {
public:
    void makeSound() {
        // implementation for Cat's sound
    }
};

class Dog : public Animal {
public:
    void makeSound() {
        // implementation for Dog's sound
    }
};
```

Now, we can create references to the `Animal` class and assign objects of `Cat` and `Dog` to those references:

```cpp
int main() {
    Cat cat;
    Dog dog;

    Animal& animal1 = cat; // reference to Cat object using Animal reference
    Animal& animal2 = dog; // reference to Dog object using Animal reference

    animal1.makeSound(); // Calls Cat's makeSound() function
    animal2.makeSound(); // Calls Dog's makeSound() function

    return 0;
}
```

In the above code, we create objects of `Cat` and `Dog`, and then we create `Animal` references `animal1` and `animal2` and assign the `cat` and `dog` objects to them, respectively. We can then call the `makeSound()` function on these references, which will call the respective implementation based on the actual object type.

Using references to abstract classes allows us to write more flexible code, as we can use different derived objects through the same abstract class reference without knowing their specific types at compile time.

## Conclusion
Abstract classes with references in C++ enable us to achieve polymorphism and write flexible code. By declaring pure virtual functions in abstract classes and using references to these abstract classes, we can utilize the power of inheritance and dynamic binding to handle objects of different derived classes uniformly.

Using abstract classes with references can improve code modularity and enable easy extensibility. By coding to an abstract interface, we can easily add new derived classes without having to modify any existing code that relies on the abstract class reference.

#C++ #AbstractClasses #References #Polymorphism #ObjectOrientedProgramming