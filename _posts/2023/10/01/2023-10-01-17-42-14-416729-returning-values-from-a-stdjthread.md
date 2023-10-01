---
layout: post
title: "Returning values from a `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

When working with multithreaded applications, it is often necessary to have a way to return values from a background thread to the calling thread. In C++, the `<thread>` library provides the `std::jthread` class, which is similar to `std::thread` but with added features for thread management. However, unlike `std::thread`, `std::jthread` doesn't provide a direct way to return values. In this blog post, we will explore some techniques to achieve this.

### Using `std::promise` and `std::future`

`std::promise` and `std::future` are two powerful classes in C++ that can be used to synchronize and communicate between different threads. We can utilize these classes along with `std::jthread` to return values.

Here's an example of how to use `std::promise` and `std::future` to return a value from a `std::jthread`:

```cpp
#include <iostream>
#include <thread>
#include <future>

int calculate_answer()
{
    // Perform some long-running computation
    std::this_thread::sleep_for(std::chrono::seconds(5));
    return 42;
}

int main()
{
    std::jthread my_thread([](std::stop_token stop_token) {
        // Use std::promise to set the result on the future
        std::promise<int> result_promise;
        std::future<int> result_future = result_promise.get_future();

        // Perform the computation
        int result = calculate_answer();

        // Check if the thread was requested to stop
        if (stop_token.stop_requested()) {
            // Handle thread interruption
            result_promise.set_exception(std::make_exception_ptr(std::runtime_error("Thread was interrupted")));
        } else {
            // Set the result on the future
            result_promise.set_value(result);
        }
    });

    // Get the result from the future
    std::future<int> result_future = my_thread.get_future();
    int result = result_future.get();

    std::cout << "Result: " << result << std::endl;

    return 0;
}
```

In the example above, we create a `std::promise` and a `std::future` to handle the return value from the `calculate_answer` function. Inside the lambda function of the `std::jthread`, we perform the computation and set the result on the promise. We also check if a stop request has been issued and handle it accordingly.

In the `main` function, we retrieve the future from the `std::jthread` and obtain the result by calling `get()` on the future. If the computation was successful, we print the result.

### Conclusion

Returning values from `std::jthread` can be achieved using `std::promise` and `std::future`. This allows for synchronization and communication between different threads in a clean and efficient way. By utilizing these C++ features, you can build more robust and efficient multithreaded applications.

#C++ #Multithreading