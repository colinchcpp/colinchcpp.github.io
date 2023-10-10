---
layout: post
title: "Queue-based breadth-first search (BFS) algorithm in C++"
description: " "
date: 2023-10-10
tags: [algorithm, graph]
comments: true
share: true
---

Breadth-First Search (BFS) is a graph traversal algorithm that explores all vertices of a graph in breadth-first order, visiting all vertices at the same level before moving to the next level. It is often used in pathfinding algorithms and network analysis.

In this blog post, I will walk you through the implementation of a queue-based BFS algorithm in C++. Let's get started!

## Graph Representation

First, we need to represent the graph using an adjacency list. An adjacency list is a collection of linked lists where each linked list represents the neighboring vertices of a particular vertex.

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Graph representation as an adjacency list
class Graph {
    int numVertices;
    vector<vector<int>> adjList;

public:
    Graph(int vertices) : numVertices(vertices) {
        adjList.resize(numVertices);
    }

    // Function to add an edge between two vertices
    void addEdge(int src, int dest) {
        adjList[src].push_back(dest);
        adjList[dest].push_back(src);
    }

    // Function to perform BFS traversal
    void BFS(int startVertex) {
        vector<bool> visited(numVertices, false);
        queue<int> bfsQueue;

        // Mark the starting vertex as visited and enqueue it
        visited[startVertex] = true;
        bfsQueue.push(startVertex);

        while (!bfsQueue.empty()) {
            int currVertex = bfsQueue.front();
            bfsQueue.pop();

            cout << currVertex << " ";

            // Enqueue all adjacent vertices of the current vertex
            for (int adjVertex : adjList[currVertex]) {
                if (!visited[adjVertex]) {
                    visited[adjVertex] = true;
                    bfsQueue.push(adjVertex);
                }
            }
        }
    }
};
```

## Test the Algorithm

Now, let's test our BFS algorithm with a sample graph. We'll create a graph with 6 vertices and add edges between them.

```cpp
int main() {
    Graph graph(6);
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 3);
    graph.addEdge(2, 4);
    graph.addEdge(2, 5);

    cout << "BFS traversal starting from Vertex 0: ";
    graph.BFS(0);

    return 0;
}
```

The output of the above code will be:

```
BFS traversal starting from Vertex 0: 0 1 2 3 4 5
```

## Conclusion

In this blog post, we implemented a queue-based Breadth-First Search (BFS) algorithm in C++. BFS is a fundamental algorithm in graph theory and is widely used in various applications. It allows us to explore a graph in breadth-first order, visiting all vertices at the same level before moving to the next level.

I hope you found this implementation helpful. Feel free to modify and extend it based on your own requirements. Happy coding!

\#algorithm #graph #bfs