---
layout: post
title: "Creating functors for custom memory allocation in C++"
description: " "
date: 2023-09-14
tags: [include, MemoryAllocation]
comments: true
share: true
---

Functors, also known as function objects, are objects that can be treated as if they were functions. They can be invoked using the function call operator `()`. This makes them versatile and enables them to encapsulate custom logic, including memory allocation and deallocation.

To create a functor for custom memory allocation in C++, you can define a class or a struct and overload the function call operator. Let's take a look at an example:

```cpp
#include <iostream>

class CustomAllocator {
public:
    void* operator()(size_t size) {
        void* memory = std::malloc(size);
        std::cout << "CustomAllocator allocated " << size << " bytes of memory" << std::endl;
        return memory;
    }

    void operator()(void* memory) {
        std::cout << "CustomAllocator deallocated memory" << std::endl;
        std::free(memory);
    }
};

int main() {
    CustomAllocator allocator;

    // Allocate memory using the functor
    int* arr = static_cast<int*>(allocator(sizeof(int) * 10));

    // Use the allocated memory
    for (int i = 0; i < 10; ++i) {
        arr[i] = i;
    }

    // Deallocate memory using the functor
    allocator(arr);
    
    return 0;
}
```

In the above code, we define a `CustomAllocator` functor that overloads the function call operator to handle both memory allocation and deallocation. In the `operator()` function, we use `std::malloc` to allocate memory and `std::free` to deallocate it.

In the `main` function, we create an instance of `CustomAllocator` named `allocator`. We then use the functor to allocate memory for an integer array and perform some operations on it. Finally, we deallocate the memory using the same functor.

Executing this code will output the following:

```
CustomAllocator allocated 40 bytes of memory
CustomAllocator deallocated memory
```

By using a functor for custom memory allocation, you have control over how memory is allocated and deallocated in your C++ program. This can be useful in scenarios where you need specific allocation strategies, such as pooling or custom memory arenas.

#C++ #MemoryAllocation