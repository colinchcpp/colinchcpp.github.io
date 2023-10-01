---
layout: post
title: "Throttling threads with `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

In multi-threaded programming, it is often necessary to control the number of threads executing concurrently to prevent resource exhaustion or to optimize performance. Throttling threads refers to limiting the number of threads actively running at any given time.

With the advent of C++20, the C++ Standard Library introduced the `std::jthread` class, which provides a convenient way to handle threads, including thread management and cleanliness of resource handling. In this blog post, we will explore how to use `std::jthread` to throttle threads effectively.

## The Problem

Let's imagine a scenario where we have a collection of tasks that need to be performed concurrently by multiple threads. However, we need to limit the number of simultaneous threads to avoid overwhelming the system or causing contention. How can we achieve this?

## The Solution

With `std::jthread`, the solution becomes straightforward. We can use a thread pool pattern, where we create a fixed number of threads and assign tasks to them in a controlled manner. Here's an example of how this can be accomplished:

```cpp
#include <iostream>
#include <vector>
#include <thread>
#include <mutex>
#include <condition_variable>

class ThreadPool {
public:
    explicit ThreadPool(size_t numThreads)
        : threads(numThreads)
    {
        for (size_t i = 0; i < numThreads; ++i) {
            threads[i] = std::jthread([this] {
                WorkerThread();
            });
        }
    }

    template<typename Task>
    void Submit(Task&& task) {
        std::unique_lock<std::mutex> lock(mutex);
        conditionVariable.wait(lock, [this] {
            return tasks.size() < maxTasks;
        });

        tasks.emplace_back(std::forward<Task>(task));
        conditionVariable.notify_one();
    }

    void Shutdown() {
        {
            std::lock_guard<std::mutex> lock(mutex);
            shuttingDown = true;
        }

        conditionVariable.notify_all();

        for (auto& thread : threads) {
            if (thread.get_id() != std::jthread::id()) {
                thread.join();
            }
        }
    }

private:
    void WorkerThread() {
        while (true) {
            std::unique_lock<std::mutex> lock(mutex);

            conditionVariable.wait(lock, [this] {
                return shuttingDown || !tasks.empty();
            });

            if (shuttingDown) {
                return;
            }

            auto task = std::move(tasks.front());
            tasks.pop_front();

            lock.unlock();

            // Execute the task
            task();

            // Notify waiting threads that a task has completed
            conditionVariable.notify_all();
        }
    }

    size_t maxTasks = 10;
    std::vector<std::jthread> threads;
    std::deque<std::function<void()>> tasks;

    std::mutex mutex;
    std::condition_variable conditionVariable;
    bool shuttingDown = false;
};

int main() {
    ThreadPool pool(4);

    for (int i = 0; i < 20; ++i) {
        pool.Submit([i] {
            std::cout << "Task " << i << " executed by thread " << std::this_thread::get_id() << std::endl;
            std::this_thread::sleep_for(std::chrono::seconds(1));
        });
    }

    pool.Shutdown();

    return 0;
}
```

In this example, `ThreadPool` is a class that manages a pool of `std::jthread` instances. The `Submit` function is used to submit tasks to the thread pool. It limits the number of tasks by utilizing a maximum task count and a condition variable. The `Shutdown` function is called to gracefully terminate all threads once all tasks have been completed.

## Conclusion

Throttling threads is an important technique in concurrent programming. With the introduction of `std::jthread` in C++20, handling threads has become more convenient and cleaner. By implementing a thread pool and using `std::jthread` to throttle the tasks, we can efficiently manage the number of threads executing concurrently.

Using `std::jthread` not only simplifies thread management but also improves code readability and reliability. It is worth exploring and leveraging the power of this new feature in your C++ projects.

#tech #threads #jthread #concurrency