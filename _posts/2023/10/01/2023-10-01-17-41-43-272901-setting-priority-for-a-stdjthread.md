---
layout: post
title: "Setting priority for a `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

By default, a `jthread` has a priority of `std::thread::priority::normal`. However, there may be cases where you need to set a specific priority for your threads according to your application requirements.

To set the priority of a `jthread`, you can make use of the native handle returned by the `get_native_handle()` member function. However, note that this approach is platform-specific and may not be available on all systems.

Here's an example of how to set the priority of a `jthread` to the highest level on a POSIX platform:

```cpp
#include <thread>
#include <pthread.h>

int main() {
    std::jthread myThread;

    pthread_t nativeHandle = myThread.get_native_handle();

    // Set the thread priority to the highest level
    struct sched_param params;
    params.sched_priority = sched_get_priority_max(SCHED_FIFO);
    pthread_setschedparam(nativeHandle, SCHED_FIFO, &params);

    // ...
}
```

In this example, we obtain the native handle of the `jthread` using `get_native_handle()`. Then, we define a `struct sched_param` to set the desired priority level. The `sched_get_priority_max()` function returns the maximum priority value for the real-time scheduling policy, and `pthread_setschedparam()` sets the priority of the thread using the native handle.

It is important to note that thread priorities are typically platform-dependent, and not all systems may support setting thread priorities. Additionally, setting thread priorities should be done with caution as it can impact the overall system performance and fairness.

Remember to consider the specific requirements of your application and the underlying platform when setting thread priorities. Also, make sure to test and profile your application to verify the effects of thread priority adjustments. Happy coding!

#C++ #Multithreading