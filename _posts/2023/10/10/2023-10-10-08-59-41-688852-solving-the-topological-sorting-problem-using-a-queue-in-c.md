---
layout: post
title: "Solving the topological sorting problem using a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In graph theory, topological sorting is an algorithm that sorts the vertices of a directed acyclic graph (DAG) based on their dependencies. It is useful in a variety of applications such as job scheduling, task sequencing, and dependency resolution. In this blog post, we will explore how to solve the topological sorting problem using a queue in C++.

## Understanding the Topological Sorting Problem

Before diving into the solution, let's first understand the problem we are trying to solve. Given a DAG represented as an adjacency list, our goal is to find an ordering of the vertices such that for every directed edge (u, v), vertex u comes before vertex v in the ordering. This ordering is called a topological sort.

## Algorithm Description

The algorithm for topological sorting using a queue works as follows:

1. Initialize an empty queue and an empty vector to store the final topological order.
2. Calculate the in-degree of each vertex by traversing through the adjacency list. The in-degree of a vertex represents the number of incoming edges to that vertex.
3. Enqueue all vertices with in-degree 0 into the queue.
4. Repeat the following steps until the queue becomes empty:
    a. Dequeue a vertex from the queue and add it to the topological order.
    b. Decrease the in-degree of all the neighboring vertices of the dequeued vertex.
    c. If any of the neighboring vertices have in-degree 0 after the decrement, enqueue them into the queue.
5. If the topological order contains all the vertices, then the graph has a valid topological sort. Otherwise, it has a cycle.

## Code Implementation

Let's see the code implementation of the topological sort algorithm using a queue in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

vector<int> topologicalSort(vector<vector<int>>& graph) {
    int n = graph.size();
    vector<int> inDegree(n, 0); // stores in-degree of vertices
    vector<int> result; // stores the topological order
    queue<int> q; // queue for BFS traversal

    // calculate in-degree of each vertex
    for (auto adjList : graph) {
        for (int v : adjList) {
            inDegree[v]++;
        }
    }

    // enqueue vertices with in-degree 0
    for (int i = 0; i < n; i++) {
        if (inDegree[i] == 0) {
            q.push(i);
        }
    }

    // perform BFS traversal
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        result.push_back(u);

        // decrease in-degree of neighboring vertices
        for (int v : graph[u]) {
            inDegree[v]--;
            if (inDegree[v] == 0) {
                q.push(v);
            }
        }
    }

    return result;
}

int main() {
    vector<vector<int>> graph = {{1, 2}, {3}, {3}, {4}, {}};
    vector<int> topologicalOrder = topologicalSort(graph);

    cout << "Topological Order: ";
    for (int vertex : topologicalOrder) {
        cout << vertex << " ";
    }
    cout << endl;

    return 0;
}
```

## Conclusion

Topological sorting is a fundamental algorithm in graph theory that allows us to find a valid ordering of vertices in a directed acyclic graph. By using a queue for traversal and keeping track of the in-degree of vertices, we can efficiently solve the topological sorting problem in C++.