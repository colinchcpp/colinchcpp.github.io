---
layout: post
title: "Custom allocation and deallocation functions in `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [cplusplus, smartpointers]
comments: true
share: true
---

However, there might be situations where you need to use custom allocation and deallocation functions with `std::unique_ptr` and `std::shared_ptr`. This could be due to specific memory requirements or for integrating with existing code. In this blog post, we'll explore how to use custom allocation and deallocation functions with these smart pointers.

## Custom Allocation in `std::unique_ptr`

By default, `std::unique_ptr` uses the `new` operator to allocate memory. But if you need to use a custom allocation function, you can specify it as a template parameter. Let's consider an example where we want to allocate memory using a custom allocator, `myAllocator`, instead of `new`:

```cpp
template <typename T>
struct myAllocator {
    T* allocate(size_t size) {
        // Custom allocation logic here
    }

    void deallocate(T* ptr, size_t size) {
        // Custom deallocation logic here
    }
};

// Using custom allocation function with std::unique_ptr
std::unique_ptr<int, myAllocator<int>> ptr;
ptr.reset(new (ptr.get_deleter().allocate(1)) int(42));
```

In the above code, we define a custom allocator, `myAllocator`, with `allocate` and `deallocate` member functions. We then specify this custom allocator as the type for the `std::unique_ptr` using `std::unique_ptr<int, myAllocator<int>>`.

To allocate memory, we use `ptr.get_deleter().allocate(1)` to obtain a pointer to the memory allocated by the custom allocator. We then pass this pointer to `ptr.reset()` for managing the allocated memory.

## Custom Allocation in `std::shared_ptr`

Similar to `std::unique_ptr`, `std::shared_ptr` also allows us to use a custom allocation function. However, with `std::shared_ptr`, we need to provide an additional custom deallocator function as well.

Here's an example of using custom allocation and deallocation functions with `std::shared_ptr`:

```cpp
template <typename T>
struct myAllocator {
    T* allocate(size_t size) {
        // Custom allocation logic here
    }

    void deallocate(T* ptr, size_t size) {
        // Custom deallocation logic here
    }
};

// Using custom allocation and deallocation functions with std::shared_ptr
std::shared_ptr<int> ptr(
    new (myAllocator<int>().allocate(1), [](int* p) { myAllocator<int>().deallocate(p, 1); })
    int(42)
);
```

In this code, we define the same `myAllocator` struct as before. We then create a `std::shared_ptr` using custom allocation and deallocation functions.

To allocate memory, we use `myAllocator<int>().allocate(1)` and pass the result to the `new` operator. Additionally, we provide a custom deallocator lambda function as the second parameter to `new`. This lambda function will be called when there are no more references to the allocated memory, ensuring that the memory is deallocated using the custom allocator.

## Conclusion

Using custom allocation and deallocation functions with `std::unique_ptr` and `std::shared_ptr` allows for greater flexibility and integration with existing codebases. By leveraging these powerful smart pointers along with custom allocation, developers can have finer control over memory management in C++ applications.

#cplusplus #smartpointers