---
layout: post
title: "Queue-based implementation of a hash table in C++"
description: " "
date: 2023-10-10
tags: [programming]
comments: true
share: true
---

In this blog post, we will explore a queue-based implementation of a hash table in the C++ programming language. Hash tables are widely used data structures that provide efficient storage and retrieval of key-value pairs. By combining the principles of queues and hash functions, we can create a powerful and efficient implementation of a hash table.

## Table of Contents
1. [Introduction](#introduction)
2. [Hash Table Basics](#hash-table-basics)
3. [Queue-based Implementation](#queue-based-implementation)
4. [Code Example](#code-example)
5. [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>

Hash tables, also known as hash maps or dictionaries, are data structures that store key-value pairs in a table-like fashion. They utilize a hash function to map keys to their corresponding values, enabling fast retrieval.

Traditionally, hash tables are implemented using arrays, which offer constant-time access to elements. However, in scenarios where the number of elements is unknown or large, it becomes challenging to determine the optimal size of the array.

## Hash Table Basics<a name="hash-table-basics"></a>

The basic idea behind a hash table is to use a hash function to convert a key into an index that corresponds to a location in an array. Each location in the array is known as a bucket, and it can store one or more key-value pairs.

To handle collisions, where multiple keys map to the same index, we use separate chaining or linear probing. In separate chaining, each bucket contains a linked list of key-value pairs. In linear probing, if a collision occurs, we simply search for the next available location in the array.

## Queue-based Implementation<a name="queue-based-implementation"></a>

Instead of using an array, our queue-based implementation of a hash table will use a queue data structure to store the key-value pairs. 

Here's a high-level overview of the implementation:
1. We initialize a fixed-size array of queues, where the size of the array is determined based on the expected number of keys.
2. We define a hash function that takes a key as input and returns an index within the range of the array.
3. To insert a key-value pair into the hash table, we compute the hash of the key and enqueue the key-value pair into the corresponding queue.
4. To search for a key, we compute the hash of the key and search for it in the corresponding queue.
5. To delete a key, we compute the hash of the key and dequeue it from the corresponding queue.

## Code Example<a name="code-example"></a>

Here's an example implementation of a queue-based hash table in C++:

```cpp
#include <iostream>
#include <queue>

const int TABLE_SIZE = 10; // Determined based on expected number of keys

class HashTable {
private:
    std::queue<std::pair<int, std::string>> table[TABLE_SIZE];

public:
    int hash(int key) {
        return key % TABLE_SIZE;
    }

    void insert(int key, const std::string& value) {
        int index = hash(key);
        table[index].push({key, value});
    }

    std::string search(int key) {
        int index = hash(key);
        while (!table[index].empty()) {
            auto pair = table[index].front();
            if (pair.first == key) {
                return pair.second;
            }
            table[index].pop();
        }
        return "Key not found";
    }

    void remove(int key) {
        int index = hash(key);
        while (!table[index].empty()) {
            auto pair = table[index].front();
            if (pair.first == key) {
                table[index].pop();
                return;
            }
            table[index].pop();
        }
    }
};

int main() {
    HashTable hashTable;
    hashTable.insert(1, "John");
    hashTable.insert(2, "Jane");
    hashTable.insert(3, "Bob");

    std::cout << hashTable.search(2) << std::endl; // Output: "Jane"

    hashTable.remove(2);
    std::cout << hashTable.search(2) << std::endl; // Output: "Key not found"

    return 0;
}
```

In the above code example, we define a `HashTable` class that uses an array of queues `table` to store key-value pairs. The `hash` function calculates the index based on the key, and the `insert`, `search`, and `remove` functions operate on the respective queues.

## Conclusion<a name="conclusion"></a>

In this blog post, we explored a queue-based implementation of a hash table in C++. By using queues instead of arrays, we can handle collisions efficiently while providing constant-time operations for insertion, search, and deletion.

The presented code example provides a basic foundation for further customization and enhancement. Being familiar with different implementations and variations of hash tables can be valuable when working on various software engineering projects.

#programming #cpp