---
layout: post
title: "Weak pointers and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

One type of smart pointer available in C++ is `std::shared_ptr`, which uses reference counting to manage the lifetime of objects. `std::shared_ptr` keeps track of the number of shared references to an object and deallocates the memory only when all the references to it have been released. While `std::shared_ptr` provides strong ownership semantics, there are cases where you might need a different approach. This is where weak pointers and `std::weak_ptr` come into play.

`std::weak_ptr` is a type of smart pointer that provides a non-owning reference to an object managed by `std::shared_ptr`. Unlike `std::shared_ptr`, `std::weak_ptr` does not increase the reference count of the underlying object. Instead, it allows you to check if the object still exists and acquire a valid `std::shared_ptr` to it if it does. If the object has been deleted, attempting to acquire a `std::shared_ptr` from a `std::weak_ptr` results in obtaining an empty `std::shared_ptr`.

The primary use case for `std::weak_ptr` is to break cyclic dependencies between objects that could cause memory leaks. Consider a scenario where two objects hold strong references to each other using `std::shared_ptr`. This creates a cyclic dependency and leads to a memory leak because neither object can be deallocated since the reference count never reaches zero. By introducing a `std::weak_ptr` in one of the objects, the cyclic dependency is broken, and the objects can be properly deallocated when they are no longer needed.

```cpp
#include <iostream>
#include <memory>

class MyClass {
public:
    std::shared_ptr<MyClass> otherObject;

    ~MyClass() {
        std::cout << "Destructor called\n";
    }
};

int main() {
    std::shared_ptr<MyClass> obj1 = std::make_shared<MyClass>();
    std::shared_ptr<MyClass> obj2 = std::make_shared<MyClass>();

    obj1->otherObject = obj2;
    obj2->otherObject = obj1;

    std::weak_ptr<MyClass> weakPtr = obj1->otherObject;

    std::cout << "Before reset: ";
    if (auto sharedPtr = weakPtr.lock()) {
        std::cout << "Object is still valid\n";
    } else {
        std::cout << "Object has been deleted\n";
    }

    obj1->otherObject.reset();

    std::cout << "After reset: ";
    if (auto sharedPtr = weakPtr.lock()) {
        std::cout << "Object is still valid\n";
    } else {
        std::cout << "Object has been deleted\n";
    }

    return 0;
}
```

In the example code above, we create two `std::shared_ptr` objects, `obj1` and `obj2`, each holding an instance of `MyClass`. We establish a cyclic dependency by assigning `obj2` to the `otherObject` member of `obj1`, and vice versa. By introducing a `std::weak_ptr` using `weakPtr`, we can check if the object is still valid using the `lock()` function. We then reset `obj1->otherObject` to break the cyclic dependency and see the effect on the validity of the weak pointer.

Using `std::weak_ptr` in combination with `std::shared_ptr` helps ensure proper memory management in scenarios where cyclic dependencies may occur. It provides a way to check if an object still exists without increasing the reference count and causing memory leaks. Properly utilizing weak pointers can greatly enhance the robustness and efficiency of your C++ code.

#cpp #smartpointers