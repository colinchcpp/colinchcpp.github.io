---
layout: post
title: "Recursive templates for binary trees in C++"
description: " "
date: 2023-09-22
tags: [cplusplus, binarytrees]
comments: true
share: true
---

When working with binary trees in C++, it is often necessary to perform recursive operations on these data structures. One common approach is to use recursive templates, which allow for easy traversal and manipulation of binary trees.

## Recursive Template Definition

```cpp
template<typename T>
struct BinaryTreeNode {
    T data;
    BinaryTreeNode<T>* left;
    BinaryTreeNode<T>* right;
    
    BinaryTreeNode(const T& val) : data(val), left(nullptr), right(nullptr) {}
};
```

The recursive template `BinaryTreeNode` represents each node of the binary tree. It contains the data stored in the node and pointers to the left and right child nodes.

## Recursive Tree Traversal

### Preorder Traversal

```cpp
template<typename T>
void preorderTraversal(BinaryTreeNode<T>* root) {
    if (root == nullptr) {
        return;
    }
    std::cout << root->data << " ";
    preorderTraversal(root->left);
    preorderTraversal(root->right);
}
```

Preorder traversal visits the root node, then the left subtree, and finally the right subtree.

### Inorder Traversal

```cpp
template<typename T>
void inorderTraversal(BinaryTreeNode<T>* root) {
    if (root == nullptr) {
        return;
    }
    inorderTraversal(root->left);
    std::cout << root->data << " ";
    inorderTraversal(root->right);
}
```

Inorder traversal visits the left subtree, then the root node, and finally the right subtree.

### Postorder Traversal

```cpp
template<typename T>
void postorderTraversal(BinaryTreeNode<T>* root) {
    if (root == nullptr) {
        return;
    }
    postorderTraversal(root->left);
    postorderTraversal(root->right);
    std::cout << root->data << " ";
}
```

Postorder traversal visits the left subtree, then the right subtree, and finally the root node.

## Recursive Tree Construction

### Constructing a Binary Search Tree (BST)

```cpp
template<typename T>
BinaryTreeNode<T>* insert(BinaryTreeNode<T>* root, const T& value) {
    if (root == nullptr) {
        return new BinaryTreeNode<T>(value);
    }
    if (value < root->data) {
        root->left = insert(root->left, value);
    }
    else if (value > root->data) {
        root->right = insert(root->right, value);
    }
    return root;
}
```

The `insert` function constructs a binary search tree by recursively inserting nodes based on their values.

## Conclusion

Recursive templates provide a flexible and efficient way to work with binary trees in C++. With recursive traversal and construction functions, you can easily manipulate and build binary tree structures. By utilizing these techniques, you can implement a wide range of algorithms and perform various operations on binary trees.

#cplusplus #binarytrees