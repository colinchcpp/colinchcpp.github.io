---
layout: post
title: "`std::unique_ptr` and `std::shared_ptr` with polymorphic types"
description: " "
date: 2023-09-24
tags: [smartpointers, polymorphism]
comments: true
share: true
---

In C++, when dealing with dynamic memory allocation, we often use smart pointers to manage the lifetime of objects. Two commonly used smart pointer types in the C++ standard library are `std::unique_ptr` and `std::shared_ptr`. These pointers provide a safer and more convenient way to handle resources compared to raw pointers.

## `std::unique_ptr`

`std::unique_ptr` is a unique ownership smart pointer. It ensures single ownership of the resource it manages and provides automatic deallocation when the pointer goes out of scope. This type of pointer cannot be copied, only moved.

Using `std::unique_ptr` with polymorphic types requires some additional considerations. Polymorphism in C++ involves having a base class with virtual functions that can be overridden by derived classes. To support polymorphic behavior, the base class's destructor must be declared as `virtual`. This allows objects to be correctly deallocated when referencing them through a base class pointer.

Here's an example of using `std::unique_ptr` with a polymorphic type:

```cpp
class Base {
public:
    virtual ~Base() {}
    virtual void foo() = 0;
};

class Derived : public Base {
public:
    void foo() override {
        // implementation
    }
};

std::unique_ptr<Base> ptr = std::make_unique<Derived>();
ptr->foo();
```

In this example, we declare a base class, `Base`, with a virtual destructor and a pure virtual function, `foo()`. We then create a derived class, `Derived`, that overrides the `foo()` function. We create a `std::unique_ptr` of type `Base` and assign it a `std::unique_ptr` created using `std::make_unique<Derived>()`. We can then call the overridden `foo()` function through the `std::unique_ptr`.

## `std::shared_ptr`

`std::shared_ptr` is a shared ownership smart pointer. Unlike `std::unique_ptr`, `std::shared_ptr` allows multiple pointers to refer to the same object. It uses reference counting to track the number of references and automatically deallocates the object when the reference count becomes zero.

`std::shared_ptr` can also be used with polymorphic types in a similar manner:

```cpp
std::shared_ptr<Base> ptr = std::make_shared<Derived>();
ptr->foo();
```

Here, we create a `std::shared_ptr` of type `Base` and assign it a `std::shared_ptr` created with `std::make_shared<Derived>()`. We can call the `foo()` function through the `std::shared_ptr` as well.

## Conclusion

Using `std::unique_ptr` and `std::shared_ptr` with polymorphic types in C++ allows for better memory management and safer handling of resources. By following the guidelines for polymorphism with smart pointers, we can leverage the benefits of these smart pointers while still supporting polymorphic behavior. Remember to use the appropriate smart pointer type based on the ownership requirements of your code.

#cpp #smartpointers #polymorphism