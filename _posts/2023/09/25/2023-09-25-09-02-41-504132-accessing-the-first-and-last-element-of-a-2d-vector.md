---
layout: post
title: "Accessing the first and last element of a 2D vector"
description: " "
date: 2023-09-25
tags: [Vectors]
comments: true
share: true
---
title: Accessing the First and Last Element of a 2D Vector
description: Learn how to access the first and last element of a vector in C++.
tags: #CPP #Vectors
---

In C++, a vector is a dynamic array that can hold multiple elements of the same data type. Sometimes, we may need to access the first and last elements of a vector efficiently. In this blog post, we will explore how to accomplish this task for a 2D vector.

## Accessing the First Element

To access the first element of a 2D vector in C++, we can use the `at()` function or the index operator `[]`. 

Here's an example:

```cpp
{% raw %}
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> myVector = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    // Using at() function
    int firstElement = myVector.at(0).at(0);
    std::cout << "First element: " << firstElement << std::endl;

    // Using index operator []
    int firstElementIndexOp = myVector[0][0];
    std::cout << "First element (index operator): " << firstElementIndexOp << std::endl;

    return 0;
}
{% endraw %}
```

In the code above, we create a 2D vector `myVector` and initialize it with some values. We then access the first element using both the `at()` function and the index operator `[]`. The output will be:

```
First element: 1
First element (index operator): 1
```

## Accessing the Last Element

Accessing the last element of a 2D vector can be done in a similar way to accessing the first element. We can use the `back()` function or the index operator `[]` with the size of the vector minus one.

Let's see an example:

```cpp
{% raw %}
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> myVector = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    // Using back() function
    int lastElement = myVector.back().back();
    std::cout << "Last element: " << lastElement << std::endl;

    // Using index operator [] and size() function
    int lastElementIndexOp = myVector[myVector.size() - 1][myVector.back().size() - 1];
    std::cout << "Last element (index operator): " << lastElementIndexOp << std::endl;

    return 0;
}
{% endraw %}
```

In the code above, we again create a 2D vector `myVector` and initialize it with some values. We then access the last element using both the `back()` function and the index operator `[]`. The output will be:

```
Last element: 9
Last element (index operator): 9
```

In conclusion, accessing the first and last element of a 2D vector in C++ can be achieved using the `at()` function or the index operator `[]`. By understanding these methods, you can efficiently manipulate the elements of your vector as needed.