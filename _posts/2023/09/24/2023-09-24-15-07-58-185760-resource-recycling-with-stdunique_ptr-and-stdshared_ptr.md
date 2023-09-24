---
layout: post
title: "Resource recycling with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

In modern C++, managing resources such as memory or file handles is typically done using smart pointers. Two commonly used smart pointer types are `std::unique_ptr` and `std::shared_ptr`. These smart pointers provide automatic memory management and ensure that resources are released properly.

## Recycling resources with `std::unique_ptr`

`std::unique_ptr` is a smart pointer that provides unique ownership of an object. When the unique pointer goes out of scope or is explicitly reset, it automatically releases the underlying resource. However, in some cases, we might want to recycle a resource instead of releasing it completely. This can be achieved by transferring ownership of the resource from one `std::unique_ptr` to another.

Consider the following example:

```cpp
#include <iostream>
#include <memory>

class Resource {
public:
    Resource() {
        std::cout << "Resource acquired!\n";
    }

    ~Resource() {
        std::cout << "Resource released!\n";
    }

    void doSomething() {
        std::cout << "Doing something with the resource...\n";
    }
};

int main() {
    std::unique_ptr<Resource> ptr1 = std::make_unique<Resource>();
    std::unique_ptr<Resource> ptr2 = std::move(ptr1); // Transfer ownership

    if (ptr2) {
        ptr2->doSomething();
    }

    return 0;
}
```

In this example, we create a `std::unique_ptr` named `ptr1` that manages a `Resource` object. Then, we transfer ownership of the resource from `ptr1` to `ptr2` using `std::move`. By doing so, we recycle the resource instead of releasing it immediately. Finally, we check if `ptr2` is not null and call a member function on the resource.

## Recycling resources with `std::shared_ptr`

`std::shared_ptr` is another smart pointer type that provides shared ownership of an object. Unlike `std::unique_ptr`, multiple `std::shared_ptr` instances can refer to the same object. When the last `std::shared_ptr` goes out of scope or is explicitly reset, the underlying resource is deleted. However, we can recycle a shared resource by creating a new `std::shared_ptr` from an existing one.

Here's an example:

```cpp
#include <iostream>
#include <memory>

class Resource {
public:
    Resource() {
        std::cout << "Resource acquired!\n";
    }

    ~Resource() {
        std::cout << "Resource released!\n";
    }

    void doSomething() {
        std::cout << "Doing something with the resource...\n";
    }
};

int main() {
    std::shared_ptr<Resource> ptr1 = std::make_shared<Resource>();
    std::shared_ptr<Resource> ptr2 = ptr1; // Create a new shared_ptr

    {
        std::shared_ptr<Resource> ptr3 = ptr2; // Create another shared_ptr

        if (ptr3) {
            ptr3->doSomething();
        }
    }

    if (ptr2) {
        ptr2->doSomething();
    }

    return 0;
}
```

In this example, we create a `std::shared_ptr` named `ptr1` that manages a `Resource` object. Then, we create a new `std::shared_ptr` named `ptr2` by assigning `ptr1` to it. This creates another shared ownership of the resource. We also create `ptr3` inside a nested scope to demonstrate the same shared ownership.

By using these smart pointer types wisely and considering resource recycling, we can effectively manage and reuse resources in our C++ programs.

#C++ #SmartPointers