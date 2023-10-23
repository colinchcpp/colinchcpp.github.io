---
layout: post
title: "Uniform initialization with std::initializer_list in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When working with C++, it is common to initialize objects using different syntaxes and constructors. However, C++11 introduced a new feature called [uniform initialization](https://en.cppreference.com/w/cpp/language/initializer_list). One aspect of this feature is `std::initializer_list`, which allows us to initialize objects with a list of values in a more concise and flexible way. In this blog post, we will explore how to use `std::initializer_list` to initialize objects in C++.

## What is std::initializer_list?

`std::initializer_list` is an STL class template that represents a lightweight array-like container. It is designed specifically for initialization purposes and is commonly used with constructors and assignment operators. With `std::initializer_list`, we can pass multiple values to initialize an object using a simple and readable syntax.

## Using std::initializer_list for object initialization

To use `std::initializer_list`, we need to include the `<initializer_list>` header. Let's start by looking at an example using `std::initializer_list` to initialize a vector of integers:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    
    for (const auto& num : numbers) {
        std::cout << num << " ";
    }
    
    return 0;
}
```

In the above code, we create a `std::vector<int>` named `numbers` and initialize it with a list of integers using `std::initializer_list`. The syntax `{1, 2, 3, 4, 5}` represents the initializer list of integers. We can then iterate over the vector and print each element.

The output of this code will be:

```
1 2 3 4 5
```

## Using std::initializer_list for custom objects

`std::initializer_list` is not limited to primitive types; it can also be used to initialize objects of custom classes. Let's look at an example of initializing a car class using `std::initializer_list`:

```cpp
#include <iostream>

class Car {
public:
    Car(const std::string& make, const std::string& model)
        : make_(make), model_(model) {}
        
    void PrintInfo() const {
        std::cout << "Make: " << make_ << ", Model: " << model_ << std::endl;
    }
    
private:
    std::string make_;
    std::string model_;
};

int main() {
    Car myCar = {"BMW", "X5"};
    myCar.PrintInfo();
    
    return 0;
}
```

In this code, we define a `Car` class with a constructor that takes two parameters: `make` and `model`. Using `std::initializer_list`, we can initialize a `Car` object named `myCar` with the values `"BMW"` and `"X5"`. We then call the `PrintInfo()` member function to display the make and model of the car.

The output of this code will be:

```
Make: BMW, Model: X5
```

## Conclusion

Using `std::initializer_list` in C++ enables us to initialize objects with a clean and concise syntax. It improves code readability and makes object initialization more flexible. Whether it's initializing containers or custom classes, `std::initializer_list` is a powerful feature to simplify object initialization in C++.