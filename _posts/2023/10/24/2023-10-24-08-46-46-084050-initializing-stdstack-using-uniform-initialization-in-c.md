---
layout: post
title: "Initializing std::stack using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, the `std::stack` container provides a way to implement the stack data structure. It is a part of the Standard Template Library (STL) and abstracts away the underlying container implementation, allowing for easy stack operations such as push and pop.

In this blog post, we will explore how to initialize a `std::stack` object using uniform initialization in C++. Uniform initialization was introduced in C++11 and allows for concise and consistent initialization of objects.

## Initializing a stack with the default container

The default container type used by `std::stack` is `std::deque`. To initialize a stack using uniform initialization, we can simply enclose the elements in braces `{}` as follows:

```cpp
std::stack<int> myStack {1, 2, 3, 4, 5};
```

In the above example, we have initialized a `std::stack` object named `myStack` with integers 1, 2, 3, 4, and 5. The stack will be populated in the order specified, with 1 on top of the stack and 5 at the bottom.

## Initializing a stack with a different container

If you wish to use a different container type, such as `std::vector` or `std::list`, you can specify it during initialization as well. Here's an example:

```cpp
std::stack<int, std::vector<int>> myStack {1, 2, 3, 4, 5};
```

In the above code snippet, we have specified that the stack should use `std::vector` as the underlying container. Again, the stack will be populated in the order specified, with 1 on top and 5 at the bottom.

## Conclusion

Using uniform initialization, we can easily initialize a `std::stack` object with elements, making our code more concise and readable. Whether using the default `std::deque` container or specifying a different container type, the initialization process remains straightforward.

Uniform initialization is just one of the many features that C++ provides to make our code more elegant and expressive. Exploring and utilizing such features can help us write cleaner and more maintainable code.

I hope this blog post has been helpful in understanding how to initialize a `std::stack` using uniform initialization in C++. Happy coding!

References:
- [std::stack - C++ Reference](https://en.cppreference.com/w/cpp/container/stack)
- [Uniform Initialization in C++](https://en.cppreference.com/w/cpp/language/initialization)