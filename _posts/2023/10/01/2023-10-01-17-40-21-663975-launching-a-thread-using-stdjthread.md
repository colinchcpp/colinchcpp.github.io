---
layout: post
title: "Launching a thread using `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

Multithreading is a powerful technique in programming that allows us to perform multiple tasks concurrently. In C++, the Standard Library provides us with the `std::jthread` class, introduced in C++20, which simplifies the process of launching a thread.

The `std::jthread` class is an improvement over `std::thread` as it automatically joins the launched thread upon destruction, which helps prevent resource leaks and makes it easier to manage threads in C++ programs. Let's see how we can use `std::jthread` to launch a thread:

```cpp
#include <iostream>
#include <thread>

void myFunction() {
    // Code to be executed in the new thread
    std::cout << "Hello from the new thread!" << std::endl;
}

int main() {
    // Launching a thread using std::jthread
    std::jthread myThread(myFunction);

    // Main thread continues its execution
    std::cout << "Hello from the main thread!" << std::endl;

    // Joining the thread automatically at the end of the block

    return 0;
}
```

In the example code above, `myFunction` represents the task that we want to execute in a separate thread. We launch a thread using `std::jthread` by passing the function or callable object as a constructor argument. The `myThread` object automatically joins the thread upon destruction, ensuring proper cleanup.

By running the program, you will see the following output:

```
Hello from the main thread!
Hello from the new thread!
```

As you can see, the main thread continues its execution while the new thread executes the function `myFunction` concurrently.

In conclusion, the `std::jthread` class simplifies the process of launching and managing threads in C++ programs. It automatically joins the launched thread upon destruction, which helps prevent resource leaks and provides a convenient way to handle multithreading tasks. Consider using `std::jthread` whenever you need to launch a thread in your C++ code.

#cpp #multithreading