---
layout: post
title: "Queue-based approach for printing the top view of a binary tree in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

<!-- Table of Contents -->
## Table of Contents

- [Introduction](#introduction)
- [Implementation](#implementation)
- [Code](#code)
- [Conclusion](#conclusion)

## Introduction

The top view of a binary tree refers to the nodes that are visible when viewed from the top. In other words, it is the leftmost node of every level in the tree. Implementing a queue-based approach allows us to efficiently print the top view of a binary tree in C++.

## Implementation

To print the top view of a binary tree, we can leverage a queue for level order traversal and a map to store the horizontal distance of each node from the root. By traversing the tree level by level and keeping track of the horizontal distance, we can print the leftmost node of each level in the tree.

## Code

```cpp
#include <iostream>
#include <queue>
#include <map>

using namespace std;

// Structure to represent a binary tree node
struct Node {
    int data;
    Node* left;
    Node* right;
};

// Function to create a new binary tree node
Node* createNode(int data) {
    Node* newNode = new Node();
    if (!newNode) {
        cout << "Memory error\n";
        return nullptr;
    }
    newNode->data = data;
    newNode->left = newNode->right = nullptr;
    return newNode;
}

// Function to print the top view of a binary tree
void topView(Node* root) {
    if (!root) {
        return;
    }

    queue<pair<Node*, int>> q;
    map<int, int> m;

    q.push(make_pair(root, 0));

    while (!q.empty()) {
        Node* currentNode = q.front().first;
        int currentHorizontalDistance = q.front().second;
        q.pop();

        if (m.find(currentHorizontalDistance) == m.end()) {
            m[currentHorizontalDistance] = currentNode->data;
            cout << currentNode->data << " ";
        }
        
        if (currentNode->left) {
            q.push(make_pair(currentNode->left, currentHorizontalDistance - 1));
        }
        
        if (currentNode->right) {
            q.push(make_pair(currentNode->right, currentHorizontalDistance + 1));
        }
    }
}

int main() {
    // Create a binary tree
    Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->right = createNode(4);
    root->left->right->right = createNode(5);
    root->left->right->right->right = createNode(6);

    cout << "Top view of the binary tree: ";
    topView(root);

    return 0;
}
```

## Conclusion

By utilizing a queue-based approach, we can efficiently print the top view of a binary tree in C++. This approach allows us to traverse the tree level by level and keep track of the horizontal distance of each node from the root. Feel free to modify and experiment with the provided code to suit your requirements.