---
layout: post
title: "Waiting for a `std::jthread` to finish execution"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

To wait for a `std::jthread` to finish, you can use the `join()` member function. This function blocks the current thread until the associated `std::jthread` has finished executing. Here's an example:

```cpp
#include <iostream>
#include <thread>

void myThreadFunction()
{
    // Simulating some work
    std::this_thread::sleep_for(std::chrono::seconds(3));
    std::cout << "Thread execution complete." << std::endl;
}

int main()
{
    std::jthread myThread(myThreadFunction); // Creating a std::jthread

    // Some other code here...

    myThread.join(); // Waiting for the thread to finish

    // Proceed with the rest of the program

    return 0;
}
```

In this code snippet, we have a `myThreadFunction` that is executed by a `std::jthread` created in the `main` function. After creating the thread, we can perform other tasks, knowing that the `std::jthread` will continue executing in the background. 

To wait for the thread to finish, we call the `join()` function on the `std::jthread` object. This will block the main thread until the associated thread completes its execution. After the `join()` call, we can proceed with the rest of our program.

Remember, calling `join()` is important to ensure that the program doesn't exit before the thread finishes, as that would lead to undefined behavior.

Make sure to handle any exceptions that might be thrown when using `std::jthread` to ensure proper cleanup.