---
layout: post
title: "Swapping elements in a vector"
description: " "
date: 2023-09-25
tags: [programming]
comments: true
share: true
---

In programming, there are many cases where we need to swap two elements in an array or a container like a vector. Swapping elements is a common operation that allows us to rearrange the order of elements in a collection.

In this blog post, we will explore how to swap elements in a vector using different approaches in C++. Let's get started!

### Approach 1: Using std::swap

The simplest way to swap elements in a vector is by using the `std::swap` function provided by the C++ Standard Library. This function takes two references as arguments and swaps their values.

```cpp
std::vector<int> vec {1, 2, 3, 4, 5};

std::swap(vec[1], vec[3]);

// Output: [1, 4, 3, 2, 5]
```

In the example above, we have a vector `vec` and we want to swap the elements at indices 1 and 3. By calling `std::swap(vec[1], vec[3])`, the values at indices 1 and 3 are swapped, resulting in the updated vector `[1, 4, 3, 2, 5]`.

### Approach 2: Using std::iter_swap

Another approach to swapping elements in a vector is by utilizing the `std::iter_swap` function. This function swaps the values of two iterators.

```cpp
std::vector<int> vec {1, 2, 3, 4, 5};

auto it1 = vec.begin() + 1;
auto it2 = vec.begin() + 3;

std::iter_swap(it1, it2);

// Output: [1, 4, 3, 2, 5]
```

In the above example, we obtain the iterators `it1` and `it2` pointing to the elements we want to swap, which are at indices 1 and 3. By calling `std::iter_swap(it1, it2)`, the values at these iterators get swapped, resulting in the updated vector `[1, 4, 3, 2, 5]`.

### Conclusion

Swapping elements in a vector is a common operation that can be achieved using different approaches in C++. Whether you choose to use `std::swap` or `std::iter_swap`, both options provide simple and efficient ways to rearrange the order of elements in a vector.

By mastering these swapping techniques, you'll have more flexibility and control over the contents of your vectors, opening up a wide range of possibilities for manipulating and organizing data.

#programming #cpp