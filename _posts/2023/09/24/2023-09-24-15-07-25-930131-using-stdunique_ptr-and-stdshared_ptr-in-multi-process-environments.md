---
layout: post
title: "Using `std::unique_ptr` and `std::shared_ptr` in multi-process environments"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When working with multi-process environments, it is important to consider how memory is managed between processes. C++ provides two smart pointers, `std::unique_ptr` and `std::shared_ptr`, that can be helpful in such scenarios. 

## `std::unique_ptr`
`std::unique_ptr` is used to manage ownership of dynamically allocated objects. It follows an exclusive ownership model, where only one `std::unique_ptr` can own an object at a given time. In a multi-process environment, each process will have its own memory space, so each process should manage its own resources separately.

To use `std::unique_ptr` in a multi-process environment, each process should create its own instance of `std::unique_ptr` and manage its own dynamically allocated objects. This ensures that memory is dealt with independently by each process, avoiding conflicts between processes.

```cpp
#include <memory>

void processA()
{
    std::unique_ptr<int> uniquePtrA(new int(42));
    // Process A owns the memory allocated for the integer
    // ...
}

void processB()
{
    std::unique_ptr<int> uniquePtrB(new int(64));
    // Process B owns the memory allocated for the integer
    // ...
}
```

## `std::shared_ptr`
`std::shared_ptr` is used for shared ownership of dynamically allocated objects. It maintains a reference count and allows multiple `std::shared_ptr` instances to point to the same object. In a multi-process environment, when processes need to share a dynamically allocated object, `std::shared_ptr` can be a useful choice.

However, `std::shared_ptr` requires synchronization mechanisms to ensure that the object is correctly shared between processes. The simplest way to achieve this is by using an inter-process communication mechanism, such as shared memory, along with a synchronization mechanism, like a semaphore or a mutex.

Here is an example of using `std::shared_ptr` in a multi-process environment with shared memory:

```cpp
#include <memory>
#include <unistd.h>
#include <sys/mman.h>
#include <fcntl.h>

void processA()
{
    int shm = shm_open("/my_shared_memory", O_CREAT | O_RDWR, 0666);
    ftruncate(shm, sizeof(int));

    void* ptr = mmap(0, sizeof(int), PROT_READ | PROT_WRITE, MAP_SHARED, shm, 0);
    std::shared_ptr<int> sharedPtr(static_cast<int*>(ptr), [](int* p) { munmap(p, sizeof(int)); shm_unlink("/my_shared_memory"); });
    
    // Process A and Process B share the same memory
    
    *sharedPtr = 42;
    // ...
}

void processB()
{
    int shm = shm_open("/my_shared_memory", O_CREAT | O_RDWR, 0666);
    ftruncate(shm, sizeof(int));

    void* ptr = mmap(0, sizeof(int), PROT_READ | PROT_WRITE, MAP_SHARED, shm, 0);
    std::shared_ptr<int> sharedPtr(static_cast<int*>(ptr), [](int* p) { munmap(p, sizeof(int)); shm_unlink("/my_shared_memory"); });
    
    // Process A and Process B share the same memory
    
    int value = *sharedPtr;
    // ...
}
```

In the above example, both `processA` and `processB` use shared memory to create a `std::shared_ptr`. They can freely access and modify the shared integer value.

## Conclusion
When working with multi-process environments, it is important to select the appropriate smart pointer for memory management. `std::unique_ptr` is suitable for exclusive ownership and ensuring that each process manages resources independently. `std::shared_ptr` can be used for shared ownership, but requires synchronization mechanisms to ensure correct sharing between processes. By applying these tools correctly, you can efficiently manage memory in multi-process environments. 

#cpp #memorymanagement