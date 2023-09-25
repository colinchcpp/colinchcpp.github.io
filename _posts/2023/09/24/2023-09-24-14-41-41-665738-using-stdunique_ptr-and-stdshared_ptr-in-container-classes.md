---
layout: post
title: "Using `std::unique_ptr` and `std::shared_ptr` in container classes"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When designing container classes in C++, it's important to choose the appropriate smart pointers to manage the lifetime of objects stored in the container. Two commonly used smart pointers are `std::unique_ptr` and `std::shared_ptr`, each with their unique ownership semantics. In this blog post, we'll explore when and how to use these smart pointers in container classes.

## `std::unique_ptr`

`std::unique_ptr` provides exclusive ownership of an object. This means that only one `std::unique_ptr` can own an object at any given time. When the owning `std::unique_ptr` is destroyed or reset, it automatically deletes the object it owns.

```cpp
#include <memory>
#include <vector>

class Container {
private:
    std::vector<std::unique_ptr<MyClass>> elements;

public:
    void addElement(std::unique_ptr<MyClass> element) {
        elements.push_back(std::move(element));
    }

    // Other member functions...
};
```

In the above example, we have a container class called `Container` that uses `std::vector` to store `std::unique_ptr` objects pointing to instances of `MyClass`. The `addElement` function takes ownership of a `std::unique_ptr` object and adds it to the vector. When the container is destroyed, all the owned `MyClass` objects will be automatically deleted.

## `std::shared_ptr`

`std::shared_ptr` provides shared ownership of an object. Multiple `std::shared_ptr` instances can share ownership of the same object. The object will only be deleted when the last `std::shared_ptr` owning it is destroyed or reset.

```cpp
#include <memory>
#include <vector>

class Container {
private:
    std::vector<std::shared_ptr<MyClass>> elements;

public:
    void addElement(std::shared_ptr<MyClass> element) {
        elements.push_back(element);
    }

    // Other member functions...
};
```

In the above example, the `Container` class uses `std::vector` to store `std::shared_ptr` objects pointing to instances of `MyClass`. The `addElement` function accepts a `std::shared_ptr` object and adds it to the vector. Since multiple `std::shared_ptr` instances can own the same object, the object will be deleted only when the last `std::shared_ptr` goes out of scope.

## Conclusion

Choosing the appropriate smart pointer for managing object ownership in container classes is crucial for memory management and avoiding potential memory leaks. Use `std::unique_ptr` when ownership of an object needs to be exclusive, and a single owner is responsible for its deletion. Use `std::shared_ptr` when multiple owners can share the same object and the object should be deleted when the last owner is destroyed.

By leveraging the power of smart pointers, we can ensure safer and more efficient memory management in our container classes.

#C++ #SmartPointers