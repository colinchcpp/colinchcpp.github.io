---
layout: post
title: "Reversing the order of words in a given string using a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this blog post, we will discuss how to reverse the order of words in a given string using a queue data structure in C++. 

## Introduction

Sometimes, we may come across a requirement where we need to reverse the order of words in a given string. One efficient way to achieve this is by using a queue. A queue is a data structure that follows the First-In-First-Out (FIFO) principle. We can leverage a queue to store the words in the string in reverse order and then reconstruct the reversed string. 

## Approach

We will follow the following steps to reverse the order of words in the given string:

1. Split the string into words.
2. Push the words onto a queue in reverse order.
3. Reconstruct the reversed string by popping words from the queue.

Here's an example implementation in C++:

```cpp
#include <iostream>
#include <string>
#include <queue>
#include <sstream>

std::string reverseString(const std::string& str) {
    std::queue<std::string> wordQueue;
    std::istringstream iss(str);
    std::string word;

    while (iss >> word) {
        wordQueue.push(word);
    }

    std::string reversedString;
    while (!wordQueue.empty()) {
        reversedString += wordQueue.front() + " ";
        wordQueue.pop();
    }

    return reversedString;
}

int main() {
   std::string str = "Hello World! I am a programmer.";
   std::string reversedString = reverseString(str);

   std::cout << "Reversed String: " << reversedString << std::endl;

   return 0;
}
```

## Explanation

In this code, we first create a `std::queue<std::string>` called `wordQueue` to store the words in reverse order. We then use `std::istringstream` to split the given string into words. 

Next, we iterate over the words and push each word onto the `wordQueue` using the `push()` function of the queue. 

Finally, we construct the reversed string by continuously appending the front word of the queue to the `reversedString`. We add a space after each word to maintain proper spacing. Finally, we `pop()` the word from the front of the queue.

## Conclusion

By using a queue, we can efficiently reverse the order of words in a given string. This approach allows us to reconstruct the reversed string in the original order without requiring extensive string manipulation.