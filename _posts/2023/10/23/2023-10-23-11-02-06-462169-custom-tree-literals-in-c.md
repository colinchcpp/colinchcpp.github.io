---
layout: post
title: "Custom tree literals in C++"
description: " "
date: 2023-10-23
tags: [DataStructures]
comments: true
share: true
---

Tree data structures are commonly used in computer science and are often represented as nested nodes. While C++ has built-in support for various data types, it doesn't provide a direct way to initialize a tree. However, by using user-defined literals, we can create our own custom tree literals in C++.

### What are user-defined literals?

User-defined literals allow us to define custom syntax for literal values of a specific type. This feature was introduced in C++11 and can be used to enhance readability and expressiveness in code.

### Creating a custom tree literal

To create a custom tree literal, we need to define an operator function that will be invoked when the compiler encounters our specific syntax. Let's say we want to represent a tree using square brackets ([]). Here's an example implementation:

```cpp
#include <iostream>
#include <vector>

struct TreeNode {
    int data;
    std::vector<TreeNode*> children;

    TreeNode(int val) : data(val) {}
};

TreeNode* operator "" _(const char* str, std::size_t size) {
    std::string input(str, size);

    if (input.empty()) {
        return nullptr;
    }

    int val = input[0] - '0';
    TreeNode* node = new TreeNode(val);

    std::size_t i = 2;
    while (i < size - 1) {
        std::size_t j = i;
        int count = 1;

        while (j < size - 1 && (count > 0 || input[j] != ',')) {
            if (input[j] == '[') {
                ++count;
            } else if (input[j] == ']') {
                --count;
            }
            ++j;
        }

        std::string child = input.substr(i, j - i);
        TreeNode* childNode = operator "" _(child.c_str(), child.size());
        node->children.push_back(childNode);

        i = j + 1;
    }

    return node;
}

void printTree(TreeNode* root) {
    if (!root) {
        return;
    }

    std::cout << root->data << " ";
    for (TreeNode* child : root->children) {
        printTree(child);
    }
}

int main() {
    // Using custom tree literals
    TreeNode* tree = "[1[2,3[4],5]]"_;
    printTree(tree);

    return 0;
}
```

In this example, we define a function `operator "" _` that handles our custom tree literals. The input string is parsed recursively to create a tree as per the specified syntax. The `printTree` function demonstrates how we can traverse and print the tree.

### Usage of custom tree literals

With the custom tree literal defined, we can now initialize a tree using the specified syntax:

```cpp
TreeNode* tree = "[1[2,3[4],5]]"_;
```

Here, we represent a tree with root value 1. It has two children: nodes with values 2 and 3. The node with value 3 has a child with value 4. Finally, the node with value 1 also has a child with value 5.

### Benefits of custom tree literals

Custom tree literals offer a concise and intuitive way to represent complex tree structures in code. They provide improved readability and reduce the boilerplate code required for tree initialization.

### Conclusion

By utilizing user-defined literals in C++, we can create custom tree literals that simplify the process of tree initialization. This allows for more straightforward and expressive code when working with tree data structures. Custom tree literals enhance code readability and reduce the complexity of tree initialization in C++.

For more details, refer to the [C++ user-defined literals documentation](https://en.cppreference.com/w/cpp/language/user_literal). #C++ #DataStructures