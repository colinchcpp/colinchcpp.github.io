---
layout: post
title: "Implementing a queue-based least common ancestor (LCA) algorithm in C++"
description: " "
date: 2023-10-10
tags: [programming]
comments: true
share: true
---

In this blog post, we will explore how to implement a queue-based Least Common Ancestor (LCA) algorithm in C++. The LCA algorithm is used to find the lowest common ancestor of two nodes in a binary tree.

## Introduction to the LCA Problem

The LCA problem is often encountered in tree-based data structures and algorithms. Given a binary tree and two nodes `a` and `b`, the LCA algorithm aims to find the lowest (i.e., deepest) common ancestor of `a` and `b` in the tree.

## Approach: Queue-Based LCA Algorithm

One common approach to solve the LCA problem is by using a queue-based algorithm. The steps involved in the algorithm are as follows:

1. Start by pushing the root node of the binary tree into a queue.
2. While the queue is not empty, perform the following steps:
   - Pop the front node from the queue.
   - Check if the popped node is either equal to `a` or `b`. If so, store it as a potential common ancestor.
   - Push the left and right children of the popped node into the queue, if they exist.
   - Repeat until the queue is empty or both `a` and `b` are found.
3. If both `a` and `b` are found, return the last stored common ancestor. Otherwise, return `nullptr` to indicate that no common ancestor exists.

## Implementation in C++

Let's proceed with the implementation of the queue-based LCA algorithm in C++:

```cpp
#include <iostream>
#include <queue>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* findLCA(TreeNode* root, TreeNode* a, TreeNode* b) {
    if (!root || !a || !b) {
        return nullptr;
    }

    std::queue<TreeNode*> q;
    TreeNode* lca = nullptr;

    q.push(root);
    while (!q.empty()) {
        TreeNode* curr = q.front();
        q.pop();

        if (curr == a || curr == b) {
            if (!lca) {
                lca = curr;
            } else {
                return lca;
            }
        }

        if (curr->left) {
            q.push(curr->left);
        }
        if (curr->right) {
            q.push(curr->right);
        }
    }

    return nullptr;
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    // Find the LCA of nodes with values 4 and 6
    TreeNode* node1 = root->left->left;
    TreeNode* node2 = root->right->left;
    TreeNode* lca = findLCA(root, node1, node2);

    if (lca) {
        std::cout << "The LCA of " << node1->val << " and " << node2->val << " is " << lca->val << std::endl;
    } else {
        std::cout << "No common ancestor found." << std::endl;
    }

    return 0;
}
```

## Conclusion

In this blog post, we have explored how to implement a queue-based LCA algorithm in C++. By using a queue, we can efficiently traverse the binary tree and find the lowest common ancestor of two given nodes. The implementation provided can be easily integrated into your C++ programs to solve the LCA problem in a queue-based manner.

#programming #C++