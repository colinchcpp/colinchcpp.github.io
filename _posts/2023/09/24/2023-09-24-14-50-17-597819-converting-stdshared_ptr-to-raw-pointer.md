---
layout: post
title: "Converting `std::shared_ptr` to raw pointer"
description: " "
date: 2023-09-24
tags: [include, SmartPointers]
comments: true
share: true
---

When working with smart pointers in C++, `std::shared_ptr` is a commonly used class that provides automatic memory management. However, there are cases where you may need to convert a `std::shared_ptr` to a raw pointer. In this blog post, we'll explore how to safely convert a `std::shared_ptr` to a raw pointer and discuss the potential pitfalls.

## Converting a `std::shared_ptr` to a Raw Pointer

To convert a `std::shared_ptr` to a raw pointer, you can use the `get` function. Here's an example:

```cpp
#include <memory>

int main() {
    std::shared_ptr<int> sharedPtr = std::make_shared<int>(42);

    int* rawPtr = sharedPtr.get();

    // Use the raw pointer

    return 0;
}
```

In the code snippet above, we create a `std::shared_ptr` called `sharedPtr` using the `std::make_shared` function. Then, we use the `get` function to obtain the raw pointer pointing to the same memory location as the `std::shared_ptr`. We assign the raw pointer to a variable called `rawPtr` and can use it as a regular raw pointer.

## Important Considerations

When converting a `std::shared_ptr` to a raw pointer, it's important to keep the following considerations in mind:

1. **Ownership**: The raw pointer obtained by `get` function **does not** manage the lifetime of the object it points to. If the `std::shared_ptr` goes out of scope or is destructed while the raw pointer is still used, it can result in a dangling pointer and undefined behavior.

2. **Lifetime Extension**: Converting a `std::shared_ptr` to a raw pointer should be done with caution. If possible, prefer to keep the `std::shared_ptr` in scope for as long as it's required to avoid potential memory access issues.

## Conclusion

In this blog post, we learned how to convert a `std::shared_ptr` to a raw pointer using the `get` function. However, it's important to be aware of the potential pitfalls, such as ownership issues and lifetime extension, when working with raw pointers. It's generally recommended to rely on smart pointers whenever possible, and only resort to using raw pointers when necessary.

#C++ #SmartPointers #RawPointers