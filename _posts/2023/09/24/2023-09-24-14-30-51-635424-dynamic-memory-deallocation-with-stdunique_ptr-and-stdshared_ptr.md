---
layout: post
title: "Dynamic memory deallocation with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [programming, cplusplus]
comments: true
share: true
---

In C++, dynamic memory allocation is a common practice when managing resources like objects, arrays, or even raw memory. However, manual memory deallocation can be error-prone and lead to memory leaks or access violations. To overcome these issues, C++ provides smart pointers like `std::unique_ptr` and `std::shared_ptr` that automatically deallocate memory when it is no longer needed.

## `std::unique_ptr`

`std::unique_ptr` is a smart pointer that provides exclusive ownership of an object or an array. Once the ownership of a resource is transferred to a `std::unique_ptr`, it is responsible for deallocating the memory when it goes out of scope. Let's look at an example:

```cpp
void processObject() {
    std::unique_ptr<Object> objectPtr(new Object()); // Create a unique_ptr to manage Object

    // ...
    // Use the object
    // ...

    // No need to manually deallocate memory here
    // unique_ptr will automatically delete the object
}

int main() {
    processObject();
    // ...
    return 0;
}
```

In the example above, `std::unique_ptr` manages the memory for the `Object` class. When `objectPtr` goes out of scope, the destructor of `std::unique_ptr` is automatically called, which in turn deallocates the memory for the `Object`. This ensures safe and automatic memory management without any manual intervention.

## `std::shared_ptr`

Unlike `std::unique_ptr`, `std::shared_ptr` allows multiple pointers to manage the same resource. It uses reference counting to keep track of the number of active references to an object. The memory is deallocated when the last `std::shared_ptr` owning the resource goes out of scope. Let's see an example:

```cpp
void processSharedObject() {
    std::shared_ptr<SharedObject> sharedPtr(new SharedObject()); // Create a shared_ptr to manage SharedObject

    // ...
    // Use the shared object
    // ...
}

int main() {
    processSharedObject();
    // ...
    return 0;
}
```

In this example, `std::shared_ptr` is used to manage the `SharedObject`. Even though the `sharedPtr` variable goes out of scope in the `processSharedObject` function, the memory is not immediately deallocated. The memory is deallocated only when the last reference to the `SharedObject` is destroyed.

## Conclusion

Smart pointers like `std::unique_ptr` and `std::shared_ptr` provide a higher level of abstraction and safety when dealing with dynamic memory allocation. They eliminate the need for manual memory deallocation and help prevent common memory management issues like memory leaks. By utilizing these smart pointers, you can write safer and more reliable code.

#programming #cplusplus