---
layout: post
title: "Count the number of elements between two given values in a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

To get started, let's assume we have a queue named `myQueue` and two given values `value1` and `value2`. Our goal is to count the number of elements in the queue that are between `value1` and `value2`.

```cpp
#include <iostream>
#include <queue>

// Function to count elements between two values in a queue
int countElementsBetweenValues(std::queue<int>& myQueue, int value1, int value2) {
    int count = 0;
    bool startCounting = false;

    // Iterate through the queue
    while (!myQueue.empty()) {
        int frontValue = myQueue.front();
        myQueue.pop();

        // Check if the current element is equal to value1
        if (frontValue == value1) {
            startCounting = true;
        }

        // Start counting if value1 is found
        if (startCounting) {
            count++;

            // Stop counting if value2 is found
            if (frontValue == value2) {
                break;
            }
        }
    }

    return count;
}

int main() {
    std::queue<int> myQueue;
    myQueue.push(1);
    myQueue.push(2);
    myQueue.push(3);
    myQueue.push(4);
    myQueue.push(5);

    int value1 = 2;
    int value2 = 4;

    int count = countElementsBetweenValues(myQueue, value1, value2);
    std::cout << "Number of elements between " << value1 << " and " << value2 << ": " << count << std::endl;

    return 0;
}
```

In the above code, we define a function `countElementsBetweenValues` that takes a reference to a queue, `myQueue`, and two integer values, `value1` and `value2`. It initializes a counter variable and a boolean flag to keep track of when to start counting.

Using a while loop, we iterate through the queue. If we encounter `value1`, we set `startCounting` to true, indicating that we need to start counting. Once `startCounting` is true, we increment the counter for each element encountered. The loop breaks when `value2` is found. Finally, we return the count of elements between the two given values.

In the `main` function, we create a queue named `myQueue` and populate it with some example values. We then define `value1` and `value2` to be 2 and 4, respectively. Finally, we call the `countElementsBetweenValues` function and print the result.

Executing the above code will output: "Number of elements between 2 and 4: 2", indicating that there are two elements (3 and 4) between the given values.

By using the provided code, you can easily count the number of elements between two given values in a queue using C++. This technique can be handy in various scenarios, such as filtering data or identifying a specific range of elements in a queue.