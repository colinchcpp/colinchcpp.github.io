---
layout: post
title: "Check if two queues are identical in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

Here's an example of how to check if two queues are identical in C++:

```cpp
#include <iostream>
#include <queue>

bool areQueuesIdentical(std::queue<int>& queue1, std::queue<int>& queue2) {
    if (queue1.size() != queue2.size()) {
        return false;
    }

    while (!queue1.empty()) {
        if (queue1.front() != queue2.front()) {
            return false;
        }

        queue1.pop();
        queue2.pop();
    }

    return true;
}

int main() {
    std::queue<int> q1, q2;

    q1.push(1);
    q1.push(2);
    q1.push(3);

    q2.push(1);
    q2.push(2);
    q2.push(3);

    if (areQueuesIdentical(q1, q2)) {
        std::cout << "The queues are identical" << std::endl;
    } else {
        std::cout << "The queues are not identical" << std::endl;
    }

    return 0;
}
```

In the above code, we define a function `areQueuesIdentical` that takes two references to `std::queue<int>` objects. The function compares the sizes of the queues and returns `false` if they are not equal. Then, it iterates over both queues, comparing each element at the front. If any elements are different, the function returns `false`. If the loops complete without finding any differences, the function returns `true`, indicating that the queues are identical.

In the `main` function, we create two `std::queue<int>` objects, `q1` and `q2`, and push some elements into them. We then call the `areQueuesIdentical` function with these two queues and display the appropriate message based on the return value.

By using this code, you can easily check if two queues are identical in C++.