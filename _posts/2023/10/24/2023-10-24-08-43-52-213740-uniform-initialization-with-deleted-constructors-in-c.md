---
layout: post
title: "Uniform initialization with deleted constructors in C++"
description: " "
date: 2023-10-24
tags: [UniformInitialization]
comments: true
share: true
---

In C++, the Uniform Initialization syntax allows for initializing objects using `{}` braces. It provides a consistent and concise way to initialize objects regardless of their underlying types. However, there are cases where you may want to prevent certain types of initializations. This is where deleted constructors come into play.

## Deleting Constructors

In C++, constructors can be deleted using the `delete` specifier. When a constructor is deleted, it means that trying to initialize an object using that particular constructor will result in a compilation error.

Let's consider a simple example where we have a class called `Person` with private member variables `name` and `age`. We want to prevent the creation of a `Person` object without providing a value for both `name` and `age`.

```cpp
class Person {
private:
    std::string name;
    int age;

public:
    // Deleted default constructor
    Person() = delete;

    // Constructor with parameters
    Person(const std::string& name, int age)
        : name(name), age(age) {}

    // Other member functions and variables...
};
```

In the example above, the default constructor for `Person` is explicitly marked as `delete`. This means that attempting to create a `Person` object without providing a name and age will result in a compilation error.

## Using Uniform Initialization

Now, let's see how Uniform Initialization works with our `Person` class:

```cpp
Person p1("John Doe", 30);   // Valid initialization
Person p2{};                // Error: Use of deleted function 'Person::Person()'
```

As you can see, initializing `Person` objects using the constructor with parameters is allowed, but attempting to initialize with an empty initializer list will result in a compilation error due to the deleted constructor.

## Conclusion

By using deleted constructors in conjunction with Uniform Initialization syntax, we can enforce certain initialization requirements for our C++ classes. This helps to prevent incorrect or unexpected object creation and ensures the integrity of the objects during their lifetime.

To learn more about deleted constructors and Uniform Initialization in C++, refer to the [C++ documentation](https://en.cppreference.com/w/cpp/language/delete) and [C++11/14/17/20 Standard](https://isocpp.org/) standards.

**#C++ #UniformInitialization**