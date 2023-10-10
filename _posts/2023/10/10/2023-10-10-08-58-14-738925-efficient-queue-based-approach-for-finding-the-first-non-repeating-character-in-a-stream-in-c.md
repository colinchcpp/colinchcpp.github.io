---
layout: post
title: "Efficient queue-based approach for finding the first non-repeating character in a stream in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

## Introduction
Finding the first non-repeating character in a stream of characters can be a common problem in programming. In this blog post, we will discuss an efficient queue-based approach to solve this problem using C++. We will explain the algorithm step by step and provide a code example for better understanding.

## Problem Statement
Given a stream of characters, we need to find and return the first non-repeating character at any given point.

## Approach
To efficiently solve this problem, we can use a combination of a queue and a hash map. The queue will keep track of the order in which characters appear in the stream, while the hash map will help us determine if a character is repeating or not.

1. Initialize an empty queue and an empty hash map.
2. For each character in the stream:
   - If the character is not present in the hash map:
     - Add the character to the queue.
     - Add the character as a key in the hash map with a value of 1.
   - If the character is already present in the hash map:
     - Increment the value of the key in the hash map by 1.
   - Check the front of the queue:
     - If the value of the front character in the queue is 1:
       - Return the front character as it is the first non-repeating character.
     - Otherwise, remove the front character from the queue.
3. If no non-repeating character is found, return a default value (e.g., '#').

## Code Example

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>
using namespace std;

char findFirstNonRepeatingCharacter(const string& stream) {
    queue<char> charactersQueue;
    unordered_map<char, int> countMap;

    for (char ch : stream) {
        if (countMap.find(ch) == countMap.end()) {
            charactersQueue.push(ch);
            countMap[ch] = 1;
        }
        else {
            countMap[ch]++;
            while (!charactersQueue.empty() && countMap[charactersQueue.front()] > 1) {
                charactersQueue.pop();
            }
        }
    }

    return (charactersQueue.empty() ? '#' : charactersQueue.front());
}

int main() {
    string stream = "aabbccdef";
    char firstNonRepeatingCharacter = findFirstNonRepeatingCharacter(stream);
    cout << "The first non-repeating character is: " << firstNonRepeatingCharacter << endl;
    return 0;
}
```

## Conclusion
The queue-based approach discussed in this blog post provides an efficient solution for finding the first non-repeating character in a stream using C++. By maintaining a queue and a hash map, we can keep track of the order of characters and efficiently determine which character is the first non-repeating one.