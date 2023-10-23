---
layout: post
title: "Custom linked list literals in C++"
description: " "
date: 2023-10-23
tags: [programming, cplusplus]
comments: true
share: true
---

In C++, literals are values that are directly written into the code, such as numbers or strings. However, C++ does not provide a built-in way to define custom literals for complex types like linked lists. In this article, we will explore how to create custom linked list literals in C++.

## What is a Linked List?

A linked list is a data structure that consists of a sequence of nodes. Each node contains data and a pointer (or link) to the next node in the sequence. The last node typically points to a null value to indicate the end of the list.

## Defining a Linked List Literal

To define a custom linked list literal, we can create a user-defined literal operator in C++. A user-defined literal operator allows us to define custom syntax for literal values of a particular type.

Here's an example of a custom linked list literal operator:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
};

Node operator"" _l(const char* str, std::size_t size) {
    // Parsing str and constructing the linked list

    Node* head = nullptr;
    Node* current = nullptr;

    for (std::size_t i = 0; i < size; ++i) {
        if (str[i] >= '0' && str[i] <= '9') {
            int value = str[i] - '0';
            Node* newNode = new Node{value, nullptr};

            if (head == nullptr) {
                head = newNode;
                current = newNode;
            } else {
                current->next = newNode;
                current = newNode;
            }
        }
    }

    return *head;
}

int main() {
    Node linkedList = "1234"_l;

    // Print the linked list
    Node* current = &linkedList;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;
    }

    return 0;
}
```

In this example, we define a user-defined literal operator `operator"" _l` that takes a string literal and constructs a linked list based on the characters in the string. The operator parses the string and creates a linked list with the corresponding values.

## Using the Custom Linked List Literal

To use the custom linked list literal, we can simply write the linked list values within quotes and append `_l` to indicate that we want to create a linked list literal.

In the `main` function of the above example, we create a linked list with the values "1234" using the custom literal `"1234"_l`. We then iterate over the linked list and print its values.

## Conclusion

By creating a user-defined literal operator, we can define custom syntax for creating linked list literals in C++. This allows us to easily create linked lists directly in our code without the need for explicit construction. This technique can be extended and customized to handle more complex cases based on specific requirements.

**References:**
- [C++ User-Defined Literals](https://en.cppreference.com/w/cpp/language/user_literal) #programming #cplusplus