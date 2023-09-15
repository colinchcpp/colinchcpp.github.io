---
layout: post
title: "Using `auto` with smart pointers in C++"
description: " "
date: 2023-09-15
tags: [cplusplus, smartpointers]
comments: true
share: true
---

Smart pointers are a great addition to modern C++ and provide automatic memory management, making it easier to handle resources and avoid memory leaks. When using smart pointers, the `auto` keyword can be handy to simplify your code and make it more concise.

## Declaring Smart Pointers with `auto`

To declare a smart pointer with `auto`, you can use the `std::make_unique` or `std::make_shared` functions, which return the correct type of smart pointer based on the argument provided.

Here's an example of using `auto` with `std::unique_ptr`:

```cpp
auto ptr = std::make_unique<int>(42);
```

In the above code, `auto` automatically deduces the type of `ptr` as `std::unique_ptr<int>`, which is created and initialized with the value `42`.

Similarly, you can use `auto` with `std::shared_ptr`:

```cpp
auto ptr = std::make_shared<double>(3.14);
```

Again, `auto` deduces the type of `ptr` as `std::shared_ptr<double>` and initializes it with the value `3.14`.

## Accessing Data with `auto`

Using `auto` with smart pointers not only simplifies the declaration but also makes it easier to access the underlying data without explicitly using the `get()` function.

```cpp
auto value = *ptr;
```

In the above example, `auto` deduces the type of `value` based on the type of the data pointed to by `ptr`. In this case, it will be `int` or `double`, respectively, from our previous examples. The `*` operator dereferences the smart pointer, giving direct access to the underlying data.

## Conclusion

Using `auto` with smart pointers in C++ can help simplify code and make it easier to work with. It automates type deduction when declaring the smart pointer and makes accessing the underlying data more concise. By leveraging smart pointers and the power of `auto`, you can write cleaner and safer C++ code.

#cplusplus #smartpointers