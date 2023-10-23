---
layout: post
title: "Initializing std::queue using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, you can use uniform initialization syntax to initialize `std::queue` with a list of elements. This syntax provides a more concise and readable way to initialize containers.

To initialize a `std::queue` using uniform initialization, you need to enclose the elements inside curly braces `{}` and pass them as a constructor argument.

Here's an example of how to initialize a `std::queue` using uniform initialization:

```cpp
#include <queue>

int main() {
    std::queue<int> myQueue{1, 2, 3, 4, 5};
    return 0;
}
```

In the above code snippet, we initialize a `std::queue` named `myQueue` with five integers: `1`, `2`, `3`, `4`, and `5`. The curly braces `{}` indicate that we are using uniform initialization.

Initializing `std::queue` this way allows you to easily populate the queue with initial values without explicitly calling the `push()` function for each element.

Uniform initialization syntax provides a consistent and modern way to initialize containers in C++, improving code readability and reducing the risk of errors.

It's important to note that uniform initialization for `std::queue` is available in C++11 and later versions.

To learn more about `std::queue` and other container classes in C++, refer to the [C++ documentation](https://en.cppreference.com/w/cpp/container/queue).

#cpp #C++