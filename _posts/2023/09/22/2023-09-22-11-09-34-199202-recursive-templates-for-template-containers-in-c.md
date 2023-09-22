---
layout: post
title: "Recursive templates for template containers in C++"
description: " "
date: 2023-09-22
tags: [RecursiveTemplates]
comments: true
share: true
---

When working with template containers in C++, it can be beneficial to have the ability to create recursive templates. Recursive templates allow for the creation of containers that can hold elements of the same type or containers of the same type. This flexibility provides a powerful mechanism for storing and manipulating complex data structures.

## Recursive Container Template

Let's start by defining a recursive container template called `RecursiveContainer`. This template can hold either an element of type `T` or another instance of `RecursiveContainer<T>`.

```cpp
template <typename T>
class RecursiveContainer {
public:
    // Constructor for an element of type T
    RecursiveContainer(const T& element) : m_element(element) {}

    // Constructor for a recursive container of type RecursiveContainer<T>
    RecursiveContainer(const RecursiveContainer<T>& container) : m_container(container) {}

    // Getter function to get the stored element
    T getElement() const {
        return m_element;
    }

    // Getter function to get the stored container
    RecursiveContainer<T> getContainer() const {
        return m_container;
    }

private:
    T m_element;
    RecursiveContainer<T> m_container;
};
```

## Usage Examples

### Storing Elements

We can use the `RecursiveContainer` template to store elements of the same type. Let's see an example:

```cpp
RecursiveContainer<int> container1(5);
RecursiveContainer<double> container2(3.14);
RecursiveContainer<std::string> container3("Hello");

int element1 = container1.getElement();                  // Retrieves the stored element (5)
double element2 = container2.getElement();               // Retrieves the stored element (3.14)
std::string element3 = container3.getElement();          // Retrieves the stored element ("Hello")
```

### Storing Containers

We can also use the `RecursiveContainer` template to store containers of the same type. Let's see an example:

```cpp
RecursiveContainer<int> container1(RecursiveContainer<int>(10));
RecursiveContainer<double> container2(RecursiveContainer<double>(2.71));
RecursiveContainer<std::string> container3(RecursiveContainer<std::string>("World"));

RecursiveContainer<int> nestedContainer = container1.getContainer();             // Retrieves the stored container (RecursiveContainer<int>(10))
int nestedElement = nestedContainer.getElement();               // Retrieves the stored element from the nested container (10)
```

## Conclusion

Recursive templates in C++ provide a powerful tool for creating flexible and dynamic container templates. By allowing containers to store either elements of the same type or other containers of the same type, it enables the creation of complex data structures. With the presented `RecursiveContainer` template, you can easily store and manipulate elements or containers, providing a versatile solution to your programming needs.

#C++ #RecursiveTemplates