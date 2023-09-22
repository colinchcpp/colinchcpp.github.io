---
layout: post
title: "Recursive templates for template classes in C++"
description: " "
date: 2023-09-22
tags: [templates]
comments: true
share: true
---

In C++, templates provide a powerful mechanism for generic programming. They allow us to write code that can handle different types without explicitly specifying them. Template classes are particularly useful when we want to reuse code for multiple types.

One interesting technique we can use with template classes is recursive templates. Recursive templates enable us to define template classes that can be used with nested templates of the same type. This recursive behavior allows us to create complex data structures or algorithms.

Let's take a look at an example of a recursive template class in C++.

```cpp
template <typename T>
class LinkedList {
public:
    T value;
    LinkedList<T>* next;

    LinkedList(T value) : value(value), next(nullptr) {}

    void addNext(T value) {
        if (next == nullptr) {
            next = new LinkedList<T>(value);
        } else {
            next->addNext(value);
        }
    }

    void printAll() {
        std::cout << value << " ";
        if (next != nullptr) {
            next->printAll();
        }
    }
};
```

In the above example, we define a `LinkedList` template class. Each instance of the `LinkedList` class holds a value of type `T` and a pointer to the next element in the list.

The `addNext` function allows us to add new elements to the linked list by recursively creating new instances of `LinkedList` and updating the `next` pointer accordingly.

The `printAll` function recursively prints all the values in the linked list.

To use the `LinkedList` template class, we can instantiate it with different types, such as `int`, `double`, or even custom types. Here's an example:

```cpp
int main() {
    LinkedList<int> list(1);
    list.addNext(2);
    list.addNext(3);
    list.addNext(4);

    list.printAll();
    return 0;
}
```

In this example, we create a `LinkedList` of integers and add a few elements. Finally, we print all the elements using the `printAll` function.

Recursive templates give us the flexibility to create complex data structures or algorithms that can work with different types. It allows us to leverage the power of generic programming in C++.

#cpp #templates