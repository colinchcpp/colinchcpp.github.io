---
layout: post
title: "Implementing a queue-based iterative deepening depth-first search (IDDFS) algorithm in C++"
description: " "
date: 2023-10-10
tags: [programming, algorithm]
comments: true
share: true
---

In this blog post, we will learn how to implement an **Iterative Deepening Depth-First Search (IDDFS)** algorithm using a **queue** data structure in C++. This algorithm is particularly useful for traversing and searching a tree or graph data structure efficiently. 

## Table of Contents
- [Introduction to IDDFS](#introduction-to-iddfs)
- [Implementing IDDFS in C++](#implementing-iddfs-in-c)
- [Time Complexity Analysis](#time-complexity-analysis)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction to IDDFS
Iterative Deepening Depth-First Search (IDDFS) is a search algorithm that combines the advantages of both breadth-first search (BFS) and depth-first search (DFS) algorithms. It performs a DFS with a depth limit, incrementing the limit gradually until the goal state is reached or all nodes have been explored.

The main advantage of IDDFS is that it uses memory efficiently, unlike BFS, which can quickly consume a large amount of memory for deep levels of the search tree. IDDFS operates in a depth-first manner, allowing it to explore deeper levels of the graph while still keeping memory requirements low.

## Implementing IDDFS in C++
To implement IDDFS using a queue data structure in C++, we can follow these steps:

1. Define a graph data structure to represent the problem domain.
2. Implement a `depthLimitedSearch` function that performs a depth-limited search from a given node, up to a specified depth limit.
3. Implement the main `IDDFS` function that iteratively increases the depth limit and calls `depthLimitedSearch`.
4. Use a queue to store the nodes to be explored in each iteration of IDDFS.

```cpp
#include <iostream>
#include <queue>
#include <vector>

// Define a graph data structure
class Graph {
    int numVertices;
    std::vector<std::vector<int>> adjList;

public:
    Graph(int num) : numVertices(num), adjList(num) {}

    void addEdge(int src, int dest) {
        adjList[src].push_back(dest);
    }

    void depthLimitedSearch(int node, int depthLimit) {
        std::cout << node << " ";

        if (depthLimit <= 0)
            return;

        for (int adjNode : adjList[node]) {
            depthLimitedSearch(adjNode, depthLimit - 1);
        }
    }

    void IDDFS(int start, int goal, int maxDepth) {
        for (int depthLimit = 0; depthLimit <= maxDepth; depthLimit++) {
            std::queue<int> queue;
            queue.push(start);

            while (!queue.empty()) {
                int node = queue.front();
                queue.pop();

                if (node == goal) {
                    std::cout << "Goal found at depth: " << depthLimit << std::endl;
                    return;
                }

                if (depthLimit > 0) {
                    for (int adjNode : adjList[node]) {
                        queue.push(adjNode);
                    }
                }
            }
        }

        std::cout << "Goal not found within the depth limit." << std::endl;
    }
};

int main() {
    Graph graph(7);
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 5);
    graph.addEdge(2, 6);

    int start = 0;
    int goal = 6;
    int maxDepth = 3;

    std::cout << "Iterative Deepening Depth-First Search (IDDFS)" << std::endl;
    std::cout << "Start: " << start << ", Goal: " << goal << ", Max Depth: " << maxDepth << std::endl;
    std::cout << "Solution Path: ";
    graph.IDDFS(start, goal, maxDepth);

    return 0;
}
```

## Time Complexity Analysis
The time complexity of the IDDFS algorithm depends on the branching factor (the average number of child nodes) of the graph or tree being searched and the depth limit set. In the worst case scenario, where the goal node is at the maximum depth, the time complexity approaches *O(b^d)*, where *b* is the branching factor and *d* is the maximum depth. However, IDDFS generally performs better than a pure DFS or BFS search, as it gradually increases the depth limit and cuts off the search early when the goal is found.

## Conclusion
In this blog post, we implemented the Iterative Deepening Depth-First Search (IDDFS) algorithm using a queue data structure in C++. IDDFS provides a memory-efficient way to search a tree or graph and can be useful in various applications. By combining the advantages of both DFS and BFS algorithms, IDDFS allows for efficient exploration of the search space.

I hope you found this article helpful in understanding how to implement the IDDFS algorithm in C++. Feel free to experiment further with different scenarios and explore different applications of this algorithm.

## References
- [Iterative Deepening Depth-First Search](https://en.wikipedia.org/wiki/Iterative_deepening_depth-first_search)
- [Depth-First Search (DFS) Algorithm](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

#programming #algorithm