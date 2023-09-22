---
layout: post
title: "Recursive template examples in C++"
description: " "
date: 2023-09-22
tags: [recursion]
comments: true
share: true
---

When working with complex data structures or algorithms, it is often useful to utilize recursive templates in C++. Recursive templates allow us to define functions or classes that can operate on structures of varying levels of complexity. In this blog post, we will explore some examples of recursive templates in C++.

## Example 1: Calculating the Factorial

Let's start with a classic example of using recursive templates to calculate the factorial of a number.

```cpp
template <int N>
struct Factorial {
    static const int value = N * Factorial<N - 1>::value;
};

template<>
struct Factorial<0> {
    static const int value = 1;
};
```

In this example, we define a `Factorial` struct with a template parameter `N` to represent the input number. The recursive template specialization is used to handle the base case when `N` is 0, which returns 1. For any other value of `N`, the value is calculated as `N` multiplied by the factorial of `N-1`.

## Example 2: Summing the Elements of an Array

Next, let's look at an example of using recursive templates to compute the sum of elements in an array.

```cpp
template <typename T, size_t N>
T ArraySum(const std::array<T, N>& arr) {
    return arr[N - 1] + ArraySum<T, N - 1>(arr);
}

template <typename T>
T ArraySum(const std::array<T, 1>& arr) {
    return arr[0];
}
```

In this example, we define a function `ArraySum` that takes an `std::array` as input. The recursive template specialization is used to handle the base case when the size of the array is 1. In this case, the function simply returns the single element. For arrays with more than 1 element, the function recursively calls itself with a smaller subarray, and adds the last element of the current subarray to the sum of the rest of the subarray.

## Conclusion

Recursive templates in C++ provide a powerful mechanism for working with complex data structures and algorithms. By utilizing template specialization and recursive calls, we can create flexible and efficient code that can handle structures of varying complexity. These examples demonstrate how recursive templates can be used to calculate the factorial of a number and sum the elements of an array. Experimenting with recursive templates can further enhance your C++ programming skills and enable you to tackle more complex problems efficiently.

\#cpp \#recursion