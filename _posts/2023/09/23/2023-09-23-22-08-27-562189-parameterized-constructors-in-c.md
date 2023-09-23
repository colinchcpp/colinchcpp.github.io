---
layout: post
title: "Parameterized Constructors in C++"
description: " "
date: 2023-09-23
tags: [include, Constructors]
comments: true
share: true
---

In object-oriented programming, a constructor is a special member method of a class that is executed when an object of that class is created. Constructors are responsible for initializing the data members of the class.

C++ allows the creation of parameterized constructors, which are constructors that can accept arguments. These arguments can be used to initialize the data members of the class with specified values.

To define a parameterized constructor in C++, follow these steps:

1. Declare the constructor in the class definition, inside the public section, specifying the desired parameters.

```cpp
class MyClass {
public:
  MyClass(int value1, float value2);
};
```

2. Define the constructor outside the class definition, using the `Class::Constructor` syntax.

```cpp
MyClass::MyClass(int value1, float value2) {
  // Initialize data members with the given values
}
```

3. Inside the constructor, assign the given values to the appropriate data members of the class.

```cpp
MyClass::MyClass(int value1, float value2) {
  data_member1 = value1;
  data_member2 = value2;
}
```

Here's an example that demonstrates the usage of a parameterized constructor:

```cpp
#include <iostream>

class Rectangle {
private:
  int width;
  int height;

public:
  Rectangle(int w, int h) {
    width = w;
    height = h;
  }

  int calculateArea() {
    return width * height;
  }
};

int main() {
  Rectangle rectangle(5, 10);
  std::cout << "Area: " << rectangle.calculateArea() << std::endl;
  return 0;
}
```

In the example above, the `Rectangle` class has a parameterized constructor that takes two arguments: `width` and `height`. The constructor initializes the `width` and `height` data members with the given values. The `calculateArea()` member function calculates and returns the area of the rectangle.

Using parameterized constructors allows for more flexibility when creating objects of a class, as the objects can be initialized with specific values right at the time of creation.

#C++ #Constructors