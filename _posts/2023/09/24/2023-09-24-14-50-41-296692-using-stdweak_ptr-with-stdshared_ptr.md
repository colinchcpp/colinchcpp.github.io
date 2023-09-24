---
layout: post
title: "Using `std::weak_ptr` with `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

When working with smart pointers in C++, it is common to use `std::shared_ptr` for shared ownership of an object. However, there are situations where you may need to break the ownership cycle to avoid memory leaks. This is where `std::weak_ptr` comes into play.

## What is `std::weak_ptr`

`std::weak_ptr` is a non-owning smart pointer that can be used to observe or access an object that is managed by a `std::shared_ptr`. Unlike `std::shared_ptr`, `std::weak_ptr` does not control the lifetime of the object. It provides a way to check if the object still exists before using it.

## Why use `std::weak_ptr`

Using `std::weak_ptr` can help you break ownership cycles between objects. These cycles occur when two or more objects hold a `std::shared_ptr` to each other, preventing them from being deallocated.

By using `std::weak_ptr`, you can obtain a `std::shared_ptr` when needed, but without contributing to the reference count. This allows the objects to be destroyed when no longer needed, preventing memory leaks.

## Example usage

```cpp
#include <iostream>
#include <memory>

class Node {
public:
    std::weak_ptr<Node> next;

    Node() {
        std::cout << "Node created\n";
    }

    ~Node() {
        std::cout << "Node destroyed\n";
    }
};

int main() {
    std::shared_ptr<Node> node1 = std::make_shared<Node>();
    std::shared_ptr<Node> node2 = std::make_shared<Node>();

    node1->next = node2;
    node2->next = node1;

    std::cout << "Before releasing shared pointers\n";

    node1.reset();
    node2.reset();

    std::cout << "After releasing shared pointers\n";

    return 0;
}
```

In this example, we create two `Node` objects and make them point to each other using `std::shared_ptr`. However, since we are using `std::weak_ptr` for the `next` member, the reference count doesn't increase. When we release the shared pointers, the `Node` objects are destroyed correctly, even though they have a circular reference.

## Conclusion

Using `std::weak_ptr` in conjunction with `std::shared_ptr` provides a powerful mechanism to handle shared ownership in C++. By breaking ownership cycles, you can prevent memory leaks and ensure the correct destruction of objects. Incorporating `std::weak_ptr` into your code can improve its robustness and memory management capabilities.

#C++ #SmartPointers