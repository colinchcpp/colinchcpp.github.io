---
layout: post
title: "How to create a `std::jthread` object in C++20"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

## Creating a std::jthread

To create a `std::jthread`, we can simply instantiate the class with a callable object that represents the function to be executed as a separate thread:

```cpp
#include <iostream>
#include <thread>

void myThreadFunction() {
    std::cout << "Hello from the thread!" << std::endl;
}

int main() {
    std::jthread myThread(myThreadFunction);
    
    // Waits for the thread to complete its execution
    myThread.join();
    
    return 0;
}
```

In the code above, we define a simple function `myThreadFunction` that will be executed by the `std::jthread` object. We then create a `std::jthread` instance `myThread` by passing the function as an argument.

Upon executing the `join()` function, the main thread waits for `myThread` to complete its execution before proceeding further. This ensures that the program doesn't terminate before the thread finishes its work.

## Key features of std::jthread

The `std::jthread` class provides several useful features compared to `std::thread`. Some of the key features include:

- Automatic join on destruction: If you forget to call `join()` explicitly, the `std::jthread` object will automatically join the thread on destruction. This helps prevent resource leaks and makes the code more robust.

- Interruption support: `std::jthread` supports thread interruption through the `request_stop()` member function, allowing you to gracefully stop the thread's execution.

- Move semantics: Like `std::thread`, `std::jthread` supports move semantics, allowing you to transfer ownership of the thread to another `std::jthread` object.

## Conclusion

The introduction of `std::jthread` in C++20 provides a more user-friendly and safer way to manage threads compared to the lower-level `std::thread` class. It combines the benefits of automatic joining on destruction, interruption support, and move semantics. By using `std::jthread`, you can write more robust and efficient multithreaded code in C++20.

#C++ #Multithreading