---
layout: post
title: "Casting between smart pointers with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [cplusplus, smartpointers]
comments: true
share: true
---

Smart pointers are an essential tool in modern C++ programming for managing dynamic memory and avoiding memory leaks. The two most commonly used smart pointers are `std::unique_ptr` and `std::shared_ptr`. `std::unique_ptr` is used when ownership of an object needs to be transferred to a single entity, while `std::shared_ptr` is used when multiple entities need to share ownership of an object.

In some cases, you may need to cast between different types of smart pointers, such as when converting a `std::unique_ptr` to a `std::shared_ptr` or vice versa. This can be done using the `std::dynamic_pointer_cast` function or by creating a new smart pointer using the appropriate constructor.

### Casting from `std::unique_ptr` to `std::shared_ptr`

To cast from a `std::unique_ptr` to a `std::shared_ptr`, you can use the `std::shared_ptr` constructor that takes a `std::unique_ptr` as an argument. Here's an example:

```cpp
std::unique_ptr<int> uniquePtr = std::make_unique<int>(10);
std::shared_ptr<int> sharedPtr = std::shared_ptr<int>(std::move(uniquePtr));
```

In the example above, we create a `std::unique_ptr` called `uniquePtr` that manages an `int` object. We then move the ownership of the `uniquePtr` to the `std::shared_ptr` called `sharedPtr` using the `std::shared_ptr` constructor. The `std::move` function is used to transfer the ownership of the `uniquePtr` to the `std::shared_ptr`.

### Casting from `std::shared_ptr` to `std::unique_ptr`

Casting from a `std::shared_ptr` to a `std::unique_ptr` is a bit more involved because transferring ownership from multiple entities to a single entity can potentially lead to memory leaks. To safely perform the cast, you can use the `std::shared_ptr` member function `std::shared_ptr::get()` to obtain a raw pointer and then create a new `std::unique_ptr` from it. Here's an example:

```cpp
std::shared_ptr<int> sharedPtr = std::make_shared<int>(20);
std::unique_ptr<int> uniquePtr = std::unique_ptr<int>(sharedPtr.get());
```

In the above example, we create a `std::shared_ptr` called `sharedPtr` that manages an `int` object. We then obtain a raw pointer to the managed object using the `sharedPtr.get()` function. Finally, we create a new `std::unique_ptr` called `uniquePtr` using the obtained raw pointer.

### Conclusion

Casting between different types of smart pointers in C++ can be achieved by using the appropriate constructor or functions provided by the standard library. It is important to handle ownership properly when casting between smart pointers to avoid memory leaks and ensure correct behavior in your programs.

#cplusplus #smartpointers