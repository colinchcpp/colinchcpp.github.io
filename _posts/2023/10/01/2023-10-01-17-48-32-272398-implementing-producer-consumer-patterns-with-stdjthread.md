---
layout: post
title: "Implementing producer-consumer patterns with `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

In concurrent programming, the producer-consumer pattern is commonly used to handle communication between two threads - one thread produces data and the other thread consumes the data. 

With the introduction of C++20, the new `std::jthread` class provides a convenient way to manage threads and their lifetimes. Let's see how we can use `std::jthread` to implement the producer-consumer pattern.

## Producer

```cpp
#include <iostream>
#include <queue>
#include <mutex>
#include <condition_variable>
#include <chrono>
#include <random>
#include <thread>

std::queue<int> dataQueue;
std::mutex mtx;
std::condition_variable cv;

void producer()
{
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<int> dist(1, 100);

    for (int i = 0; i < 10; ++i) {
        int data = dist(gen);

        std::lock_guard<std::mutex> lock(mtx);
        dataQueue.push(data);
        std::cout << "Produced: " << data << std::endl;

        cv.notify_one(); // Notify consumer
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
}
```

In the `producer` function, we generate random data using `std::random_device` and `std::mt19937`. We then push the data into the `dataQueue` using a mutex for synchronization. We also notify the consumer thread using the `cv.notify_one()` method after producing each item.

## Consumer

```cpp
void consumer()
{
    while (true) {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, []{ return !dataQueue.empty(); });

        int data = dataQueue.front();
        dataQueue.pop();
        std::cout << "Consumed: " << data << std::endl;

        lock.unlock();
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
    }
}
```

In the `consumer` function, we create a loop that waits for the `dataQueue` to not be empty. We use a `std::unique_lock` along with the `cv.wait()` method to wait until data is available for consumption. Once data is available, we retrieve it from the queue, print it out, and then sleep for one second before consuming the next item.

## Putting it all together

```cpp
int main()
{
    std::jthread producerThread(producer);
    std::jthread consumerThread(consumer);

    producerThread.join();
    consumerThread.join();

    return 0;
}
```

In the `main()` function, we create two `std::jthread` objects - one for the producer and one for the consumer. We pass the respective functions `producer` and `consumer` as arguments to the thread constructors. After starting the threads, we wait for them to finish by calling `join()` on each of the threads. Finally, we return 0 to indicate successful termination.

By using the `std::jthread` class along with mutexes and condition variables, we can easily implement the producer-consumer pattern in C++. This allows for safe communication and synchronization between producer and consumer threads.

#C++ #Multithreading