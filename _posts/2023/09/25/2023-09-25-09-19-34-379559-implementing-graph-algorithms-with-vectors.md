---
layout: post
title: "Implementing graph algorithms with vectors"
description: " "
date: 2023-09-25
tags: [graph]
comments: true
share: true
---

Graphs are a fundamental data structure in computer science and are used to model relationships between entities. Implementing graph algorithms efficiently is crucial for solving a wide range of problems such as pathfinding, clustering, and network analysis. In this article, we will explore how to implement graph algorithms using vectors, a versatile container in many programming languages.

## Graph Representation using Vectors

A graph can be represented using an adjacency list or an adjacency matrix. In this article, we will focus on the adjacency list representation, which is simpler and more memory-efficient for sparse graphs.

In C++, we can use the `std::vector` container to represent the adjacency list. Each element of the `std::vector` will itself be a `std::vector` containing the neighbors of a particular vertex.

```cpp
#include <vector>

using namespace std;

class Graph {
  int numVertices;
  vector<vector<int>> adjList;

public:
  Graph(int numVertices) : numVertices(numVertices), adjList(numVertices) {}

  void addEdge(int src, int dest) {
    adjList[src].push_back(dest);
    // If the graph is undirected, add the reverse edge as well
    adjList[dest].push_back(src);
  }

  vector<int> getNeighbors(int vertex) {
    return adjList[vertex];
  }
};
```

## Breadth-First Search (BFS)

Breadth-First Search (BFS) is an algorithm used to traverse or search a graph in a breadthward motion. It starts at the root vertex and explores all the neighbor vertices at the current level before moving to the next level.

```cpp
vector<int> breadthFirstSearch(const Graph& graph, int startVertex) {
  vector<int> visited(graph.numVertices);
  vector<int> result;
  queue<int> q;

  visited[startVertex] = true;
  q.push(startVertex);

  while (!q.empty()) {
    int currentVertex = q.front();
    q.pop();
    result.push_back(currentVertex);

    vector<int> neighbors = graph.getNeighbors(currentVertex);
    for (int neighbor : neighbors) {
      if (!visited[neighbor]) {
        visited[neighbor] = true;
        q.push(neighbor);
      }
    }
  }

  return result;
}
```

## Depth-First Search (DFS)

Depth-First Search (DFS) is an algorithm used to traverse or search a graph in a depthward motion. It explores as far as possible along each branch before backtracking.

```cpp
vector<int> depthFirstSearch(const Graph& graph, int startVertex) {
  vector<int> visited(graph.numVertices);
  vector<int> result;

  dfsUtil(graph, startVertex, visited, result);

  return result;
}

void dfsUtil(const Graph& graph, int currentVertex, vector<int>& visited, vector<int>& result) {
  visited[currentVertex] = true;
  result.push_back(currentVertex);

  vector<int> neighbors = graph.getNeighbors(currentVertex);
  for (int neighbor : neighbors) {
    if (!visited[neighbor]) {
      dfsUtil(graph, neighbor, visited, result);
    }
  }
}
```

## Conclusion

Implementing graph algorithms using vectors provides a flexible and efficient solution for working with graphs. We explored how to represent graphs using the adjacency list representation and demonstrated the implementation of Breadth-First Search (BFS) and Depth-First Search (DFS) algorithms. With this knowledge, you can now solve a wide range of graph-related problems efficiently using vectors in your preferred programming language.

#graph #algorithms