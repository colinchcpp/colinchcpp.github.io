---
layout: post
title: "`std::unique_ptr` and `std::shared_ptr` with dynamic memory allocation"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When it comes to managing dynamic memory allocation in C++, two commonly used smart pointer classes are `std::unique_ptr` and `std::shared_ptr`. These classes provide a safer and more efficient way to handle memory resources, reducing the risk of memory leaks and simplifying memory management.

## `std::unique_ptr`

`std::unique_ptr` is a smart pointer that guarantees exclusive ownership of the dynamically allocated object. It is the preferred choice when you have a single owner for a resource and want to ensure that only one pointer manages it.

Here's an example of how to use `std::unique_ptr`:

```cpp
#include <memory>

int main() {
    std::unique_ptr<int> ptr(new int(10));
    // Access the value using the dereference operator *
    int value = *ptr; 

    // ... Do something with the value

    return 0;
}
```

In the above code snippet, we create a `std::unique_ptr` named `ptr` and initialize it with a dynamically allocated integer value of 10. We can access the value using the dereference operator `*ptr`.

The beauty of `std::unique_ptr` lies in its ability to automatically deallocate the memory when it goes out of scope. You don't need to manually delete the object since the smart pointer takes care of it.

## `std::shared_ptr`

Unlike `std::unique_ptr`, `std::shared_ptr` allows multiple pointers to manage the same dynamically allocated object. It keeps track of the number of references to the resource and automatically deallocates it when the last reference goes out of scope.

Here's an example of how to use `std::shared_ptr`:

```cpp
#include <memory>

int main() {
    std::shared_ptr<int> ptr1 = std::make_shared<int>(10);
    std::shared_ptr<int> ptr2 = ptr1;

    // ... Do something with the shared pointers

    return 0;
}
```

In the above code snippet, we create two `std::shared_ptr` instances named `ptr1` and `ptr2`. `ptr1` is initialized with a dynamically allocated integer value of 10 using `std::make_shared`. We can assign `ptr1` to `ptr2` because `std::shared_ptr` supports shared ownership.

By using `std::shared_ptr`, you can avoid memory leaks caused by forgetting to deallocate memory. The memory will be released automatically once all shared pointers that own the resource are destroyed.

## Conclusion

`std::unique_ptr` and `std::shared_ptr` are powerful smart pointer classes in C++ that simplify memory management and prevent memory leaks. Using these classes reduces the chances of manual errors while dealing with dynamic memory allocation, resulting in safer and more efficient code.

#C++ #smartpointers