---
layout: post
title: "Using `std::shared_ptr` for caching purposes"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Caching is a common technique used in software development to improve performance by storing and retrieving frequently requested data in a faster access memory. One commonly used caching strategy is to store objects in memory and reuse them instead of recreating them every time they are needed.

One way to implement caching in C++ is by using the `std::shared_ptr` class from the C++ Standard Library. `std::shared_ptr` is a smart pointer that provides automatic memory management, ensuring that the object it points to is destroyed when it is no longer referenced.

To use `std::shared_ptr` for caching purposes, you can follow these steps:

## Step 1: Create a Caching Class

```cpp
#include <iostream>
#include <memory>
#include <unordered_map>

class Cache {
public:
    std::shared_ptr<DataObject> getObject(const std::string& key) {
        std::lock_guard<std::mutex> lock(mutex_);

        if (cache_.count(key) > 0) {
            std::cout << "Retrieving object from cache: " << key << std::endl;
            return cache_[key];
        }

        // If the object is not in the cache,
        // create a new object and store it in the cache
        std::cout << "Creating object: " << key << std::endl;
        std::shared_ptr<DataObject> obj = std::make_shared<DataObject>(/* ... */);
        cache_[key] = obj;
        return obj;
    }

private:
    std::unordered_map<std::string, std::shared_ptr<DataObject>> cache_;
    std::mutex mutex_;
};

class DataObject {
    // ...
};
``` 

## Step 2: Use the Caching Class

```cpp
int main() {
    Cache cache;
    
    std::shared_ptr<DataObject> obj1 = cache.getObject("key1"); // Creates and caches object
    std::shared_ptr<DataObject> obj2 = cache.getObject("key2"); // Creates and caches object

    std::shared_ptr<DataObject> obj3 = cache.getObject("key1"); // Retrieves object from cache
    
    return 0;
}
``` 

In the above example, we create a `Cache` class that uses an `std::unordered_map` to store the cached objects. The `getObject` method is used to retrieve an object with a given key. If the object is not found in the cache, a new object is created, stored in the cache, and returned. If the object is already present in the cache, it is retrieved and returned.

Using `std::shared_ptr` ensures that the cached objects are automatically deallocated when they are no longer referenced by any other code.

Using `std::shared_ptr` for caching purposes provides a convenient and safe way to implement caching in C++. It helps improve performance and reduce memory usage by reusing objects instead of creating them repeatedly.