---
layout: post
title: "References and polymorphism in C++"
description: " "
date: 2023-09-27
tags: [polymorphism]
comments: true
share: true
---

When programming in C++, references and polymorphism are important concepts to understand as they provide flexibility and improve code readability. In this blog post, we will explore what references and polymorphism are and how they can be used in C++.

## References in C++

In C++, a reference is an alias for an existing object. It provides an alternative way to access the object without creating a new copy. 

To declare a reference, use the `&` symbol after the type when defining a variable. For example:

```cpp
int x = 10;
int& ref = x;
```

Now, `ref` is a reference to the `x` variable. Any changes made using `ref` will also be reflected in `x`, and vice versa.

References are commonly used to pass variables to functions by reference, allowing the function to modify the original object. This avoids unnecessary copying of large objects.

```cpp
void increment(int& num) {
    num++;
}

int main() {
    int x = 5;
    increment(x);
    cout << x; // Output: 6
    return 0;
}
```

## Polymorphism in C++

Polymorphism is the ability of an object to take on multiple forms. In C++, polymorphism can be achieved using inheritance and virtual functions.

Inheritance is a fundamental concept in object-oriented programming that allows defining a new class based on an existing class. The derived class inherits the properties and methods of the base class.

Consider a base class called `Shape`:

```cpp
class Shape {
public:
    virtual void draw() {
        cout << "Drawing a shape" << endl;
    }
};
```

Now, we can create derived classes with their implementation of the `draw` method:

```cpp
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a circle" << endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        cout << "Drawing a square" << endl;
    }
};
```

Using polymorphism, we can store objects of derived classes in a container of the base class type:

```cpp
int main() {
    vector<Shape*> shapes;
    shapes.push_back(new Circle());
    shapes.push_back(new Square());

    for (Shape* shape : shapes) {
        shape->draw();
    }

    // Output:
    // Drawing a circle
    // Drawing a square

    return 0;
}
```

In this example, the `draw` method of the appropriate derived class is called based on the actual type of the object.

## Conclusion

References and polymorphism are powerful features in C++ that enhance code reusability and flexibility. Understanding how to use references and polymorphism effectively can greatly improve your C++ programming skills. Incorporate these concepts into your code to write more maintainable and efficient applications.

#C++ #polymorphism