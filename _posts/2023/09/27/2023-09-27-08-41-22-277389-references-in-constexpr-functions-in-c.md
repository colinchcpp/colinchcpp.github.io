---
layout: post
title: "References in constexpr functions in C++"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

By definition, constexpr functions are evaluated at compile time and their return values must be computable during the compilation process. This implies that constexpr functions cannot work with non-const references, as modifying a non-const reference requires runtime execution.

However, it is still possible to use const references within constexpr functions. In this case, the reference is treated as an immutable value, and any modifications to the data it refers to will not affect the compile-time evaluation.

Let's say we have a simple example where we want to calculate the square of a number using a constexpr function:

```cpp
constexpr int square(const int& num) {
   return num * num;
}
```

In this case, the function square takes a const reference to an integer and returns the square of that number. Since we are using a const reference, the function can be evaluated at compile time and used in situations where compile-time constants are required.

However, it's worth noting that if you pass a non-const reference to a constexpr function, it will fail to compile, as shown in this example:

```cpp
int value = 5;
constexpr int result = square(value); // Error: Non-const reference cannot be used in a constexpr function
```

To work around the limitation of non-const references in constexpr functions, you can use pointers instead. Pointers can be passed as arguments to constexpr functions, and the referenced data can be modified at runtime while still allowing for compile-time evaluation:

```cpp
constexpr int square(int* num) {
   (*num) *= (*num);
   return *num;
}

int value = 5;
constexpr int result = square(&value); // Okay: Pointer can be used in a constexpr function
```

By passing the address of the variable to the constexpr function and using a pointer parameter, we can modify the value indirectly and achieve the desired result.

In conclusion, constexpr functions in C++ have certain limitations when it comes to working with references. Non-const references cannot be used, but const references are acceptable. However, you can work around this limitation by using pointers instead.