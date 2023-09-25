---
layout: post
title: "Recursive templates for template iterators in C++"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

In C++, templates are a powerful feature that allows for generic programming. Recursive templates take this power to the next level, allowing us to create flexible and reusable code by leveraging the concept of recursion.

## What are Template Iterators?

Template iterators are a way to iterate over elements in a template container, such as a `std::vector` or a custom container class. They provide an interface to access and manipulate the elements in a container without exposing the underlying data structures.

## Recursive Template Iterators

Recursive template iterators are a technique that allows us to perform operations on each element of a container using recursive function templates. This technique is particularly useful when we want to apply the same operation to each element, without having to write separate code for each type of container.

Here's an example implementation of a recursive template iterator that iterates over elements of a container:

```cpp
template <typename Container, typename Functor>
void iterate(Container& container, Functor func) {
    for (auto& element : container) {
        func(element);
    }
}

template <typename Container, typename Functor>
struct RecursiveIterator {
    void operator()(Container& container, Functor func) {
        iterate(container, func);
    }
};

template <typename T, typename Functor>
void applyToEachElement(T& container, Functor func) {
    RecursiveIterator<T, Functor>()(container, func);
}
```

In the above code, the `iterate` function template loops through each element in the container and applies the provided functor to it. The `RecursiveIterator` struct is a simple wrapper that allows us to utilize the function template as a functor.

The `applyToEachElement` function acts as the entry point to perform the operation on each element of the container. It takes a container and a functor and invokes the `RecursiveIterator` to iterate over the elements.

## Usage Example

Let's see how we can use the recursive template iterator to apply a square function to each element of a vector of integers:

```cpp
#include <iostream>
#include <vector>

void square(int& element) {
    element *= element;
}

int main() {
    std::vector<int> numbers {1, 2, 3, 4, 5};

    applyToEachElement(numbers, square);

    for (const auto& number : numbers) {
        std::cout << number << " ";
    }

    return 0;
}
```

The output of the above code will be:
```
1 4 9 16 25
```

As you can see, the `square` function is applied to each element of the vector using the `applyToEachElement` function and the recursive template iterator. This demonstrates the power of recursive templates by allowing us to apply a common operation to different types of containers.

## Conclusion

Recursive template iterators provide a flexible and reusable way to iterate over elements of a template container in C++. By leveraging recursion, we can write generic code that works with various container types, improving code reuse and maintainability.