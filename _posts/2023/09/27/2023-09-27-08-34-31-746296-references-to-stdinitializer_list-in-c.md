---
layout: post
title: "References to std::initializer_list in C++"
description: " "
date: 2023-09-27
tags: [stdinitializelist]
comments: true
share: true
---

When it comes to initializing a container or a custom class object in C++, `std::initializer_list` can be a powerful tool. Introduced in C++11, `std::initializer_list` provides a concise and efficient way to pass a sequence of values as a single argument. It is primarily used to initialize containers like `std::vector`, `std::array`, or even user-defined classes.

## Understanding `std::initializer_list`

An `std::initializer_list` is an **immutable** sequence of elements of the same type. It behaves like a lightweight container, providing access to its elements through iterators. The elements within the initializer list cannot be modified, making it suitable for initializing const containers or for read-only access.

## Using `std::initializer_list` with Containers

Consider the following example that demonstrates the usage of `std::initializer_list` with `std::vector`:

```cpp
#include <iostream>
#include <vector>

void printNumbers(const std::initializer_list<int>& numbers) {
  for (const auto& number : numbers) {
    std::cout << number << " ";
  }
  std::cout << std::endl;
}

int main() {
  std::vector<int> numbers {1, 2, 3, 4, 5};
  printNumbers({6, 7, 8, 9, 10});

  return 0;
}
```

In this example, we define the `printNumbers` function that takes an `std::initializer_list<int>` as its argument. We then iterate over the elements of the initializer list and print them.

We can pass an initializer list directly to the function, as shown in the `main` function. Additionally, we use an initializer list to initialize the `std::vector<int>`.

## Using `std::initializer_list` with User-defined Classes

To utilize `std::initializer_list` with user-defined classes, we need to define a constructor that accepts an `std::initializer_list` parameter. Let's take a look at an example:

```cpp
#include <iostream>
#include <initializer_list>

class Point {
public:
  Point(std::initializer_list<double> coordinates) {
    for (const auto& coordinate : coordinates) {
      m_coordinates.push_back(coordinate);
    }
  }

  void printCoordinates() const {
    for (const auto& coordinate : m_coordinates) {
      std::cout << coordinate << " ";
    }
    std::cout << std::endl;
  }

private:
  std::vector<double> m_coordinates;
};

int main() {
  Point point1 {1.5, 2.0, 3.2};
  point1.printCoordinates();

  Point point2 {4.8, 5.9};
  point2.printCoordinates();

  return 0;
}
```

In this example, the `Point` class is defined with a constructor that accepts an `std::initializer_list<double>` parameter. Inside the constructor, we iterate over the initializer list and add each coordinate to the private `m_coordinates` vector.

We create two instances of the `Point` class using initializer lists and demonstrate the printing of coordinates.

## Conclusion

Using `std::initializer_list` in C++ allows for concise and efficient initialization of containers and user-defined classes. Its ability to represent sequences of values as a single argument provides code readability and simplifies initialization code. Whether you are initializing containers or creating constructors for user-defined classes, `std::initializer_list` can be a valuable tool in your C++ programming arsenal.

#C++ #stdinitializelist