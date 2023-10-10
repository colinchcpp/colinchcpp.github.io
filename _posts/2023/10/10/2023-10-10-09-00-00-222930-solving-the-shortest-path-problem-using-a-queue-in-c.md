---
layout: post
title: "Solving the shortest path problem using a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

The shortest path problem is a common problem in computer science and mathematics. It involves finding the shortest path between two nodes in a graph. One popular algorithm to solve this problem is Dijkstra's algorithm, which uses a priority queue to keep track of the nodes and their distances from the starting node.

In this tutorial, we will implement Dijkstra's algorithm using a queue in C++.

## Creating the Graph

First, let's create a simple graph with nodes and edges. We will represent the graph using an adjacency list. Here is an example graph with 6 nodes:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

// Create a structure to represent a node and its distance from the starting node
struct Node {
    int index;
    int distance;

    Node(int i, int d) : index(i), distance(d) {}
};

// Create a custom comparison function for the priority queue based on distance
class Compare {
public:
    bool operator()(const Node& n1, const Node& n2) {
        return n1.distance > n2.distance;
    }
};

// Create the graph as an adjacency list
vector<vector<pair<int, int>>> graph;

// Function to add an edge to the graph
void addEdge(int u, int v, int weight) {
    graph[u].push_back(make_pair(v, weight));
}

// Function to print the shortest path from the starting node
void printShortestPath(int* distance, int n) {
    cout << "Shortest path distances from the starting node:\n";
    for (int i = 0; i < n; i++) {
        cout << "Node " << i << ": " << distance[i] << endl;
    }
}

// Function to calculate the shortest path using Dijkstra's algorithm
void shortestPath(int startNode, int n) {
    // Create a priority queue to store the nodes
    priority_queue<Node, vector<Node>, Compare> pq;

    // Create an array to store the distance from the starting node
    int distance[n];
    for (int i = 0; i < n; i++) {
        distance[i] = INT_MAX;
    }

    // Set the distance of the starting node to 0
    distance[startNode] = 0;

    // Enqueue the starting node to the priority queue
    pq.push(Node(startNode, 0));

    // Process the nodes in the priority queue
    while (!pq.empty()) {
        // Get the node with the minimum distance
        Node currentNode = pq.top();
        pq.pop();

        // Update the distance of the adjacent nodes
        for (pair<int, int> neighbor : graph[currentNode.index]) {
            int newDistance = distance[currentNode.index] + neighbor.second;
            if (newDistance < distance[neighbor.first]) {
                distance[neighbor.first] = newDistance;
                pq.push(Node(neighbor.first, newDistance));
            }
        }
    }

    // Print the shortest path distances
    printShortestPath(distance, n);
}

int main() {
    // Initialize the graph with 6 nodes
    int n = 6;
    graph.resize(n);

    // Add edges to the graph
    addEdge(0, 1, 4);
    addEdge(0, 2, 1);
    addEdge(1, 3, 1);
    addEdge(2, 1, 2);
    addEdge(2, 3, 5);
    addEdge(3, 4, 3);
    addEdge(4, 1, 3);
    addEdge(4, 5, 2);

    // Find the shortest path from node 0
    shortestPath(0, n);

    return 0;
}
```

## Explanation

### Creating the Graph

First, we create a structure called `Node` to represent a node and its distance from the starting node. The `graph` is represented as an adjacency list where each vertex has a vector of pairs containing the adjacent vertex and the weight of the edge.

### Dijkstra's Algorithm

We then define the `shortestPath` function which takes the starting node and the number of nodes as parameters. Inside the function, we create a priority queue `pq` to store the nodes based on their distances. We also create an array `distance` to store the distance of each node from the starting node.

We initialize the `distance` array with `INT_MAX` and set the distance of the starting node to 0. We then enqueue the starting node to the priority queue.

Next, we process the nodes in the priority queue until it's empty. In each iteration, we pop the node with the minimum distance from the queue and update the distance of its adjacent nodes if a shorter path is found. We then enqueue the updated nodes to the priority queue.

After the algorithm finishes, we call the `printShortestPath` function to print the shortest path distances from the starting node.

## Conclusion

In this tutorial, we implemented Dijkstra's algorithm using a queue in C++ to solve the shortest path problem. The algorithm efficiently finds the shortest path between two nodes in a graph by using a priority queue to keep track of the nodes and their distances.