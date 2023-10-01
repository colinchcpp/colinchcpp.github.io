---
layout: post
title: "Communicating between threads using `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

## Shared Variables
Shared variables are a simple way to communicate between threads by allowing them to access and modify the same memory locations. However, using shared variables requires careful synchronization to avoid race conditions. Here's an example:

```cpp
#include <iostream>
#include <thread>

int sharedData = 0;
std::mutex mutex;

void workerThread()
{
    for (int i = 0; i < 10; ++i)
    {
        std::lock_guard<std::mutex> lock(mutex);
        sharedData += i;
    }
}

int main()
{
    std::jthread thread(workerThread);
    
    // Access the shared variable
    std::lock_guard<std::mutex> lock(mutex);
    std::cout << "Shared data: " << sharedData << std::endl;
    
    return 0;
}
```
In this example, we create a shared variable `sharedData` and a `std::mutex` for synchronization. The `workerThread` function is executed concurrently in a separate thread and increments the `sharedData` variable. In the `main` function, we lock the mutex to safely access the shared variable and print its value.

## Message Passing
Message passing involves sending data or messages between threads through a communication channel. The channel can be a thread-safe queue, a mailbox, or any other inter-thread communication mechanism. Here's an example using `std::queue` as the message passing channel:

```cpp
#include <iostream>
#include <queue>
#include <thread>
#include <condition_variable>

std::queue<int> messageQueue;
std::mutex mutex;
std::condition_variable cv;

void producerThread()
{
    // Produce some messages
    for (int i = 0; i < 10; ++i)
    {
        std::lock_guard<std::mutex> lock(mutex);
        messageQueue.push(i);
        cv.notify_one();
    }
}

void consumerThread()
{
    // Consume messages
    while (true)
    {
        std::unique_lock<std::mutex> lock(mutex);
        cv.wait(lock, [] { return !messageQueue.empty(); });
        
        int message = messageQueue.front();
        messageQueue.pop();
        lock.unlock();
        
        // Process the message
        std::cout << "Received message: " << message << std::endl;
        
        if (message == 9)
            break;
    }
}

int main()
{
    std::jthread producer(producerThread);
    std::jthread consumer(consumerThread);
    
    return 0;
}
```
In this example, we have two threads: `producerThread` and `consumerThread`. The producer thread generates messages and pushes them into the `messageQueue`, while the consumer thread continuously waits for messages to be available. Once a message is received, it is processed accordingly. The condition variable `cv` is used to synchronize the communication between the two threads.

## Conclusion
In this blog post, we explored two techniques for communicating between threads using `std::jthread` in C++. Shared variables can be used, but they require proper synchronization to avoid race conditions. Message passing, on the other hand, provides a more robust and flexible way of thread communication. Depending on your requirements, you can choose the appropriate technique to ensure effective communication and synchronization between threads.

#Threads #Concurrency