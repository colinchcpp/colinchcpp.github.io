---
layout: post
title: "Initializing static arrays with uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, static arrays can be initialized using uniform initialization syntax, which was introduced in C++11. Uniform initialization provides a more concise and consistent way to initialize arrays. 

## Initialization using braces

With uniform initialization, you can initialize a static array by enclosing the elements within curly braces. Let's see an example:

```cpp
int numbers[] = {1, 2, 3, 4, 5};
```

In the above code, we declare and initialize a static array `numbers` of type `int` with five elements: 1, 2, 3, 4, and 5.

## Partial initialization

Uniform initialization also allows partial initialization of static arrays. You can initialize only a few elements, and the remaining elements will be set to their default values. Here's an example:

```cpp
int numbers[5] = {1, 2, 3};
```

In the above code, we declare and initialize a static array `numbers` of type `int` with five elements. The first three elements are initialized with the values 1, 2, and 3, while the last two elements will be set to 0.

## Aggregate initialization

Uniform initialization works well with aggregate types, such as struct or class. You can initialize an array of structures or classes using braces. For example:

```cpp
{% raw %}
struct Point {
    int x;
    int y;
};

Point points[] = {{1, 2}, {3, 4}, {5, 6}};
{% endraw %}
```

In the above code, we define a structure `Point` with two integer members `x` and `y`. Then, we declare and initialize a static array `points` of type `Point` with three elements.

## Conclusion

Uniform initialization provides a concise and consistent way to initialize static arrays in C++. By using curly braces `{}`, you can easily initialize arrays with explicit values or partially initialize them. This syntax also works well with aggregate types.

## References

- [C++ documentation on Uniform initialization](https://en.cppreference.com/w/cpp/language/list_initialization)
- [C++ documentation on Arrays](https://en.cppreference.com/w/cpp/container/array)
- [C++ documentation on Aggregate initialization](https://en.cppreference.com/w/cpp/language/aggregate_initialization)