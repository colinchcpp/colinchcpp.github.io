---
layout: post
title: "Queue-based depth-first search (DFS) algorithm in C++"
description: " "
date: 2023-10-10
tags: [technology, algorithm]
comments: true
share: true
---

When it comes to graph traversal algorithms, Depth-First Search (DFS) is widely used. It explores as far as possible along each branch before backtracking. In this article, we will explore a queue-based implementation of the DFS algorithm using C++.

## Understanding Depth-First Search (DFS)

DFS is an algorithm used for traversing or searching tree or graph data structures. It starts at a specific node and explores as far as possible along each branch before backtracking.

The DFS algorithm can be implemented using a stack or recursion. However, for a large graph, using recursion may cause a stack overflow. To overcome this limitation, we can implement DFS using a queue.

## Queue-based DFS Algorithm Implementation

Here's an implementation of the queue-based DFS algorithm in C++:

```cpp
{% raw %}
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

void dfs(vector<vector<int>>& graph, int startNode) {
    queue<int> q;
    vector<bool> visited(graph.size(), false);

    q.push(startNode);
    visited[startNode] = true;

    while (!q.empty()) {
        int currentNode = q.front();
        q.pop();

        cout << currentNode << " ";

        for (int adjacentNode : graph[currentNode]) {
            if (!visited[adjacentNode]) {
                q.push(adjacentNode);
                visited[adjacentNode] = true;
            }
        }
    }
}

int main() {
    // Create a sample graph
    vector<vector<int>> graph = {{1, 2}, {0, 3, 4}, {0, 4, 5}, {1}, {1, 2}, {2}};

    // Starting node for DFS traversal
    int startNode = 0;

    cout << "DFS traversal: ";
    dfs(graph, startNode);

    return 0;
}
{% endraw %}
```

## How the Algorithm Works

1. Initialize a queue, a visited array, and push the starting node to the queue.
2. Mark the starting node as visited.
3. While the queue is not empty:
   - Get the front element from the queue.
   - Process the current node (in this example, we print it).
   - Get all adjacent nodes of the current node that have not been visited.
   - Mark each adjacent node as visited and enqueue it.
4. Repeat step 3 until the queue is empty.

## Conclusion

Implementing the queue-based DFS algorithm provides us with an alternative approach to traversing graphs, especially when recursion might lead to stack overflow errors. By using a queue, we can successfully explore the graph in a depth-first manner.

By understanding and implementing different graph traversal algorithms, we can efficiently solve various graph-related problems and optimize performance.

#technology #algorithm