---
layout: post
title: "Ownership transfer with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When working with modern C++, managing ownership of dynamically allocated objects is a crucial aspect of writing robust and efficient code. The C++ Standard Library provides two smart pointer classes, `std::unique_ptr` and `std::shared_ptr`, which offer easy and safe ownership transfer of dynamically allocated resources.

## `std::unique_ptr`

`std::unique_ptr` is a smart pointer that represents exclusive ownership of an object. It ensures that there is only one owner of the object at any given time. When the `std::unique_ptr` goes out of scope or is explicitly reset, it automatically deletes the managed object.

```cpp
#include <memory>

struct MyClass {
    // ...
};

int main() {
    std::unique_ptr<MyClass> uniquePtr(new MyClass());
    
    // Transfer ownership to another unique_ptr
    std::unique_ptr<MyClass> anotherUniquePtr(std::move(uniquePtr));
    
    // Reset uniquePtr (no longer owns the object)
    uniquePtr.reset();
    
    return 0;
}
```

In the example above, we create a `std::unique_ptr` pointing to a dynamically allocated object of type `MyClass`. We can transfer ownership of the object by using `std::move`, allowing us to initialize another `std::unique_ptr` with the same object. After transferring ownership, calling `reset()` on `uniquePtr` releases ownership of the object, effectively nullifying the `unique_ptr`.

## `std::shared_ptr`

`std::shared_ptr` is a smart pointer that allows multiple owners of an object. It uses reference counting to track the number of owners, and the object is deleted only when the last `std::shared_ptr` owning it is destroyed or reset.

```cpp
#include <memory>

struct MyClass {
    // ...
};

int main() {
    std::shared_ptr<MyClass> sharedPtr(new MyClass());
    
    // Transfer ownership to another shared_ptr
    std::shared_ptr<MyClass> anotherSharedPtr = sharedPtr;
    
    // Reset one shared_ptr (object still exists due to another owner)
    sharedPtr.reset();
    
    return 0;
}
```

In this example, we create a `std::shared_ptr` pointing to a dynamically allocated object. We can transfer ownership by simply assigning the `std::shared_ptr` to another variable. The reference counting mechanism ensures that as long as there is at least one `std::shared_ptr` owning the object, it remains alive.

## Conclusion

Proper management of ownership is essential for writing maintainable and error-free code. With `std::unique_ptr` and `std::shared_ptr`, you have powerful tools at your disposal for performing ownership transfer of dynamically allocated objects in a safe and efficient manner. By carefully choosing the appropriate smart pointer and using the right ownership transfer techniques, you can avoid common memory management issues and improve the overall quality of your code.

\#C++ \#SmartPointers