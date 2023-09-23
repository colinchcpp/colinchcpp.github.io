---
layout: post
title: "Constructors in Lifetime of an Object in C++"
description: " "
date: 2023-09-23
tags: [Constructors]
comments: true
share: true
---

Constructors play a crucial role in the life cycle of an object in C++. They are special member functions of a class that are invoked automatically when an object of the class is created. **Constructors are responsible for initializing the data members of an object**. In this article, we will explore the different types of constructors and their role in the lifetime of an object.

## Default Constructor ##
A **default constructor** is a constructor that takes no parameters. If a class does not have any constructors defined, the compiler generates a default constructor automatically. This constructor initializes the data members with their default values. The default constructor is invoked automatically when an object is created without any arguments.

```cpp
class MyClass {
public:
  int myInt;

  // Default Constructor
  MyClass() {
    myInt = 0; // Initialize myInt with 0
  }
};

int main() {
  MyClass obj; // Default constructor is called
  return 0;
}
```

## Parameterized Constructor ##
A **parameterized constructor** is a constructor that takes one or more parameters. It allows us to initialize the data members of an object with specified values. We can define multiple parameterized constructors with different arguments in a class, providing flexibility in object initialization.

```cpp
class Rectangle {
public:
  double length;
  double width;

  // Parameterized Constructor
  Rectangle(double len, double wid) {
    length = len;
    width = wid;
  }
};

int main() {
  Rectangle rect(4.5, 6.7); // Parameterized constructor is called
  return 0;
}
```

## Copy Constructor ##
A **copy constructor** is a special constructor that creates a new object as a copy of an existing object. It takes a reference to an object of the same class as its parameter. The copy constructor is invoked when we create a new object by initializing it with another object of the same class.

```cpp
class Person {
public:
  string name;

  // Copy Constructor
  Person(const Person& obj) {
    name = obj.name;
  }
};

int main() {
  Person person1;
  person1.name = "John";

  Person person2 = person1; // Copy constructor is called
  return 0;
}
```

Constructors ensure that an object is properly initialized before it can be used. By understanding and utilizing different types of constructors in C++, we can effectively manage the lifetime of an object. #C++ #Constructors