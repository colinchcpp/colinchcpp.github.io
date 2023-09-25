---
layout: post
title: "`std::shared_ptr` with custom allocator"
description: " "
date: 2023-09-24
tags: [stdsharedptr]
comments: true
share: true
---

`std::shared_ptr` is a popular smart pointer class in the C++ standard library that provides automatic memory management. By default, `std::shared_ptr` uses the default allocator for memory allocation and deallocation. However, sometimes you may want to use a custom allocator to manage the memory for `std::shared_ptr`.

In this blog post, we will explore how to use `std::shared_ptr` with a custom allocator in C++.

## Custom Allocator for `std::shared_ptr`

To use a custom allocator with `std::shared_ptr`, you need to create a class that satisfies the allocator requirements defined by the C++ standard.

Here's an example of a custom allocator class:

```cpp
#include <memory>

template<typename T>
struct MyAllocator {
    using value_type = T;

    MyAllocator() noexcept = default;
    template<typename U>
    MyAllocator(const MyAllocator<U>&) noexcept {}

    T* allocate(std::size_t n) {
        // Your custom allocation logic here
        return static_cast<T*>(::operator new(sizeof(T) * n));
    }

    void deallocate(T* p, std::size_t n) noexcept {
        // Your custom deallocation logic here
        ::operator delete(p);
    }
};
```

In this example, we define a custom allocator called `MyAllocator` that satisfies the requirements of the allocator concept. The `allocate` function is responsible for allocating memory, and the `deallocate` function is used for deallocating memory.

## Using `std::shared_ptr` with Custom Allocator

To use `std::shared_ptr` with a custom allocator, you need to specify the allocator type as a template parameter when creating the smart pointer. Here's an example:

```cpp
int main() {
    using CustomSharedPtr = std::shared_ptr<int, MyAllocator<int>>;
    CustomSharedPtr ptr = std::allocate_shared<int, MyAllocator<int>>(MyAllocator<int>(), 42);

    // Use the custom shared pointer
    // ...

    return 0;
}
```

In this example, we create a typedef `CustomSharedPtr` for `std::shared_ptr` that uses our custom allocator `MyAllocator<int>`. We then use `std::allocate_shared` to create a shared pointer with the provided allocator. The allocator is passed as a constructor argument along with the desired value for the shared pointer.

## Conclusion

Using `std::shared_ptr` with a custom allocator can be useful in scenarios where you need more control over memory allocation and deallocation. By implementing a custom allocator that satisfies the requirements of the allocator concept, you can use it with `std::shared_ptr` to manage memory using your own allocation logic.

#C++ #stdsharedptr #customallocator