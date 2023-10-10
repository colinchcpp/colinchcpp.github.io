---
layout: post
title: "Solving the queue reconstruction by height problem using a priority queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this blog post, we will discuss how to solve the "Queue Reconstruction by Height" problem using a priority queue in C++. This problem involves rearranging a given queue of people based on their heights and the number of people in front of them.

## Problem Statement

Given a queue of people represented by pairs of integers `(h, k)`, where `h` is the height of the person and `k` represents the number of people in front of them who have a height greater than or equal to `h`, rearrange the queue such that it is in the correct order.

## Approach

To solve this problem, we can use a priority queue as our main data structure. The idea is to sort the people in descending order of their heights and, in case of a tie, sort them in ascending order of their `k` value.

1. First, we sort the people array in descending order of their heights. If two people have the same height, we sort them in ascending order of their `k` value.
2. We create an empty priority queue.
3. We iterate through the sorted people array, and for each person, we insert them into the priority queue at index `k` (as mentioned in the problem statement). The priority queue will automatically reorder itself based on the height and `k` values.
4. Finally, we convert the priority queue back into a vector and return it as the result.

## Example Code

Here's the C++ implementation of the above approach:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

vector<pair<int, int>> reconstructQueue(vector<pair<int, int>>& people) {
    sort(people.begin(), people.end(), [](pair<int, int>& a, pair<int, int>& b) {
        if (a.first == b.first) {
            return a.second < b.second;
        }
        return a.first > b.first;
    });

    vector<pair<int, int>> result;
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    for (auto& p : people) {
        pq.push(p);
    }

    while (!pq.empty()) {
        auto p = pq.top();
        pq.pop();
        result.insert(result.begin() + p.second, p);
    }

    return result;
}

int main() {
    vector<pair<int, int>> people = {{7, 0}, {4, 4}, {7, 1}, {5, 0}, {6, 1}, {5, 2}};
    vector<pair<int, int>> result = reconstructQueue(people);

    for (const auto& p: result) {
        cout << "(" << p.first << ", " << p.second << ") ";
    }

    return 0;
}
```

## Conclusion

In this blog post, we discussed how to solve the "Queue Reconstruction by Height" problem using a priority queue in C++. We went through the approach and provided an example implementation. Using a priority queue allows us to efficiently rearrange the queue in the required order.