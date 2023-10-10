---
layout: post
title: "Implementing a queue-based LRU (Least Recently Used) cache in C++"
description: " "
date: 2023-10-10
tags: [programming, caching]
comments: true
share: true
---

When building applications, caching is often used to optimize performance by temporarily storing frequently accessed data. One popular caching strategy is the Least Recently Used (LRU) algorithm, which removes the least recently used items from the cache when it is full.

In this article, we will explore how to implement an LRU cache using a queue data structure in C++. Let's get started!

## The Queue-Based LRU Cache Class

First, let's define a class for our queue-based LRU cache. This class will have the following features:

1. A fixed size limit to manage the cache capacity.
2. A queue to track the accessed items and their order. The most recently accessed items will be at the front of the queue.
3. A map to store the key-value pairs where the keys are used to access and manipulate the cache items.

Here's the basic structure of our LRU cache class:

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>

template<typename KeyType, typename ValueType>
class LRUCache {
public:
    LRUCache(size_t capacity)
        : m_capacity(capacity) {
    }

    ValueType get(const KeyType& key) {
        if (m_cacheMap.count(key) == 0) {
            return ValueType{}; // Return default value if key does not exist.
        }

        // Update the item's position in the queue to reflect its "recently used" status.
        m_cacheQueue.remove(key);
        m_cacheQueue.push(key);

        return m_cacheMap[key];
    }

    void put(const KeyType& key, const ValueType& value) {
        if (m_cacheMap.count(key) > 0) {
            // Key already exists, update its value and position in the queue.
            m_cacheQueue.remove(key);
        } else if (m_cacheMap.size() >= m_capacity) {
            // Cache is full, evict the least recently used item.
            KeyType lruKey = m_cacheQueue.front();
            m_cacheMap.erase(lruKey);
            m_cacheQueue.pop();
        }

        // Add the new item to the cache and update its position in the queue.
        m_cacheMap[key] = value;
        m_cacheQueue.push(key);
    }

private:
    size_t m_capacity;
    std::unordered_map<KeyType, ValueType> m_cacheMap;
    std::queue<KeyType> m_cacheQueue;
};
```

## Using the LRU Cache

Now that we have our LRU cache class implemented, let's see how we can use it in our application. Here's a simple example:

```cpp
int main() {
    // Create an LRU cache with a capacity of 3.
    LRUCache<int, std::string> cache(3);

    // Add some items to the cache.
    cache.put(1, "One");
    cache.put(2, "Two");
    cache.put(3, "Three");

    // Access an item from the cache.
    std::cout << cache.get(2) << std::endl; // Output: Two

    // Add another item, exceeding the cache capacity.
    cache.put(4, "Four");

    // Access the evicted item.
    std::cout << cache.get(1) << std::endl; // Output: ""

    return 0;
}
```

In this example, we create an LRU cache with a capacity of 3 and insert three items into it. We then access an item to make it the most recently used. Finally, we add a fourth item, which evicts the least recently used item from the cache.

## Conclusion

Implementing a queue-based LRU cache can greatly improve the performance of your applications by efficiently managing frequently accessed data. By following the steps outlined in this article, you can easily implement an LRU cache using the provided C++ code.

Remember to adjust the capacity of the cache based on your specific needs and the available resources to ensure optimal performance. Happy coding!

#programming #caching