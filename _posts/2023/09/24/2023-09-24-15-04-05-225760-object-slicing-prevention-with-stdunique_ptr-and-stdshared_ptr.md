---
layout: post
title: "Object slicing prevention with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [ObjectSlicing, SmartPointers]
comments: true
share: true
---

## Introduction
In C++, object slicing can occur when a derived class object is assigned to a base class object, causing loss of derived class-specific information. This can be particularly problematic when dealing with polymorphism and dynamic binding. Luckily, C++ provides two smart pointers, `std::unique_ptr` and `std::shared_ptr`, which can help prevent object slicing. In this blog post, we will explore how these smart pointers can be used to avoid object slicing and ensure the proper handling of derived class objects.

## Object Slicing Explained
Object slicing occurs when a derived class object is assigned to a base class object, resulting in the loss of derived class-specific information. This happens because the base class object can only hold the members inherited from the base class, and any additional members or overrides introduced by the derived class are sliced away. This can lead to unexpected behavior and incorrect results when trying to access derived class-specific functionality.

Consider the following example:

```cpp
class Base {
public:
    virtual void print() const {
        std::cout << "Base" << std::endl;
    }
};

class Derived : public Base {
public:
    void print() const override {
        std::cout << "Derived" << std::endl;
    }
};

int main() {
    Derived derivedObj;
    Base baseObj = derivedObj; // Object slicing occurs here
    baseObj.print(); // Output: "Base" instead of "Derived"

    return 0;
}
```

In this example, the `Derived` class overrides the `print()` function inherited from the `Base` class. However, when the `derivedObj` is assigned to the `baseObj`, object slicing occurs, and the derived class-specific functionality is lost. Thus, calling the `print()` function on the `baseObj` prints "Base" instead of "Derived".

## Preventing Object Slicing with `std::unique_ptr`
`std::unique_ptr` is a smart pointer that provides exclusive ownership of an object. It guarantees that only one `std::unique_ptr` can point to a particular object. By using `std::unique_ptr`, we can prevent object slicing since the ownership remains with the derived class object.

Let's modify the previous example using `std::unique_ptr`:

```cpp
class Base {
public:
    virtual void print() const {
        std::cout << "Base" << std::endl;
    }
};

class Derived : public Base {
public:
    void print() const override {
        std::cout << "Derived" << std::endl;
    }
};

int main() {
    std::unique_ptr<Derived> derivedObj = std::make_unique<Derived>();
    std::unique_ptr<Base> baseObj = std::move(derivedObj);
    baseObj->print(); // Output: "Derived"

    return 0;
}
```

In this updated example, we use `std::unique_ptr<Derived>` to store the derived class object. Then, we move the ownership of the `derivedObj` to a new `std::unique_ptr<Base>`. By doing so, we ensure that the derived class-specific functionality is preserved, and no object slicing occurs.

## Preventing Object Slicing with `std::shared_ptr`
`std::shared_ptr` is a smart pointer that allows multiple pointers to refer to the same object. It keeps track of how many shared pointers are pointing to the object and automatically deletes the object when its reference count reaches zero. By using `std::shared_ptr`, we can also prevent object slicing.

Let's modify the example using `std::shared_ptr`:

```cpp
class Base {
public:
    virtual void print() const {
        std::cout << "Base" << std::endl;
    }
};

class Derived : public Base {
public:
    void print() const override {
        std::cout << "Derived" << std::endl;
    }
};

int main() {
    std::shared_ptr<Derived> derivedObj = std::make_shared<Derived>();
    std::shared_ptr<Base> baseObj = derivedObj;
    baseObj->print(); // Output: "Derived"

    return 0;
}
```

In this updated example, we create a `std::shared_ptr<Derived>` to store the derived class object. Then, we assign it to a `std::shared_ptr<Base>`. The shared ownership mechanism of `std::shared_ptr` ensures that the original object is not sliced, and both pointers can access the derived class-specific functionality.

## Conclusion
Object slicing can introduce unexpected behavior and should be avoided when dealing with polymorphism and derived class objects. By utilizing `std::unique_ptr` and `std::shared_ptr`, we can prevent object slicing and ensure the proper handling of derived class objects. These smart pointers provide the necessary mechanisms for exclusive ownership and shared ownership, respectively, helping us maintain the integrity of derived class-specific functionality.

#C++ #ObjectSlicing #SmartPointers