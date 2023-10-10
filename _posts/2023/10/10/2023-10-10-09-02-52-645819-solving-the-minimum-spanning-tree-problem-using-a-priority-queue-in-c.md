---
layout: post
title: "Solving the minimum spanning tree problem using a priority queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

The **minimum spanning tree** (MST) problem is a classic algorithmic problem in computer science and graph theory. It involves finding the minimum cost set of edges that connects all nodes in a connected, undirected graph. One efficient way to solve this problem is by using a priority queue data structure.

In this blog post, we will explore how to solve the MST problem using a priority queue in C++. We will begin by explaining the basic concepts of minimum spanning trees, and then dive into the implementation details using a priority queue.

## What is a Minimum Spanning Tree?

A minimum spanning tree of a connected, undirected graph is a tree that connects all nodes of the graph together with the minimum total edge weight. It is a subgraph of the original graph that is both acyclic and connected.

The MST problem is often encountered in various applications, such as network design, clustering analysis, and transportation planning. Efficient algorithms for finding the minimum spanning tree are widely employed in these areas.

## Solving MST using a Priority Queue

One popular algorithm for solving the MST problem is **Prim's algorithm**, which uses a priority queue to select the next edge with the minimum weight. The algorithm builds the minimum spanning tree incrementally, by adding the cheapest edge at each step.

### Implementation Steps

Here are the implementation steps for solving the MST problem using Prim's algorithm and a priority queue in C++:

1. Create a graph representation using adjacency list or adjacency matrix.
2. Initialize a priority queue to store the edges with their weights. The queue should be ordered in ascending order based on the edge weight.
3. Select an arbitrary node to start the algorithm and mark it as visited.
4. Add all edges connected to the selected node to the priority queue.
5. Repeat until all nodes are visited:
   - Remove the minimum weight edge from the priority queue.
   - If the endpoint of the edge is not visited:
     - Add the edge to the minimum spanning tree.
     - Mark the endpoint as visited.
     - Add all edges connected to the endpoint to the priority queue.
6. The minimum spanning tree is the set of edges added in step 5.

### Example Code

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Structure to represent an edge
struct Edge {
    int src, dest, weight;
};

// Custom comparator for edges based on weight
struct CompareEdges {
    bool operator()(const Edge& e1, const Edge& e2) {
        // Compare edges based on weight
        return e1.weight > e2.weight;
    }
};

// Function to find the minimum spanning tree using Prim's algorithm
vector<Edge> findMinimumSpanningTree(const vector<vector<pair<int, int>>>& graph) {
    int numNodes = graph.size();
    vector<bool> visited(numNodes, false);
    priority_queue<Edge, vector<Edge>, CompareEdges> pq;
    vector<Edge> mst;

    // Start with node 0
    visited[0] = true;
    
    // Add all edges connected to node 0 to the priority queue
    for(const pair<int, int>& edge : graph[0]) {
        pq.push({0, edge.first, edge.second});
    }

    while(!pq.empty()) {
        Edge currentEdge = pq.top();
        pq.pop();

        int dest = currentEdge.dest;

        // Check if the destination node is already visited
        if(!visited[dest]) {
            // Add the edge to the minimum spanning tree
            mst.push_back(currentEdge);

            // Mark the destination node as visited
            visited[dest] = true;

            // Add all edges connected to the destination node to the priority queue
            for(const pair<int, int>& edge : graph[dest]) {
                pq.push({dest, edge.first, edge.second});
            }
        }
    }

    return mst;
}

int main() {
    // Example usage
    vector<vector<pair<int, int>>> graph = {
        {{1, 10}, {2, 6}},
        {{0, 10}, {2, 3}, {3, 4}},
        {{0, 6}, {1, 3}, {3, 8}},
        {{1, 4}, {2, 8}}
    };

    vector<Edge> minimumSpanningTree = findMinimumSpanningTree(graph);

    // Print the minimum spanning tree
    cout << "Minimum Spanning Tree:" << endl;
    for(const Edge& edge : minimumSpanningTree) {
        cout << edge.src << " -- " << edge.dest << "  (" << edge.weight << ")" << endl;
    }

    return 0;
}
```

### Conclusion

In this blog post, we discussed how to solve the minimum spanning tree problem using Prim's algorithm and a priority queue in C++. We explained the basic concepts of minimum spanning trees, outlined the steps for the algorithm's implementation, and provided example code.

Solving the minimum spanning tree problem is crucial for various real-world applications, and understanding efficient algorithms like Prim's algorithm can greatly aid in solving graph-related problems.