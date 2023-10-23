---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is a fundamental operation in programming, and the C++ Standard Library provides various sorting algorithms to efficiently sort collections of elements. By default, these algorithms use the less-than (`<`) operator to compare elements during the sorting process. However, there are cases where you may need to sort objects using a custom sorting criteria or using literals other than the less-than operator.

In this blog post, we will explore how to perform custom sorting using custom literals in C++. We will start by understanding the basic concepts of sorting and then dive into implementing custom sorting criteria.

## Table of Contents
- [The Basics of Sorting](#the-basics-of-sorting)
- [Custom Sorting Criteria](#custom-sorting-criteria)
- [Sorting Using Custom Literals](#sorting-using-custom-literals)
- [Conclusion](#conclusion)

## The Basics of Sorting

Before we delve into custom sorting literals, let's take a brief look at the basics of sorting in C++.

The C++ Standard Library provides the `std::sort` function, which is a highly efficient sorting algorithm based on the **introsort** algorithm. By default, `std::sort` uses the less-than (`<`) operator to compare elements and sort them in ascending order.

```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> numbers = {4, 2, 7, 1, 5};
    
    std::sort(numbers.begin(), numbers.end());
    
    // numbers: {1, 2, 4, 5, 7}
    
    return 0;
}
```

In the above code snippet, we have a vector of integers `numbers`, and we sort it using `std::sort`. After sorting, the `numbers` vector will contain elements in ascending order.

## Custom Sorting Criteria

Sometimes, the default sorting criteria may not be suitable for our needs. For example, suppose we have a collection of custom objects where we want to sort them based on a specific member variable rather than their natural ordering. In such cases, we can provide a custom sorting predicate to `std::sort` to define our own sorting logic.

```cpp
#include <algorithm>
#include <vector>

struct Person {
    std::string name;
    int age;
};

bool sortByAge(const Person& p1, const Person& p2) {
    return p1.age < p2.age;
}

int main() {
    std::vector<Person> people = {{"Alice", 25}, {"Bob", 30}, {"Charlie", 20}};
    
    std::sort(people.begin(), people.end(), sortByAge);
    
    // people: {{"Charlie", 20}, {"Alice", 25}, {"Bob", 30}}
    
    return 0;
}
```

In the above code snippet, we define a custom sorting predicate `sortByAge` that compares `Person` objects based on their `age` member variable. We pass this predicate as the third argument to `std::sort` to perform sorting using our custom criteria.

## Sorting Using Custom Literals

Sometimes, we may need to sort objects based on a literal other than the less-than operator. For instance, we may want to sort strings in a case-insensitive manner or sort complex numbers based on their magnitudes.

To achieve this, we can define custom literals and compare objects based on those literals. This allows us to have more control over the sorting process.

```cpp
#include <algorithm>
#include <string>

bool caseInsensitiveCompare(const std::string& s1, const std::string& s2) {
    // Perform case-insensitive comparison logic here
}

int main() {
    std::vector<std::string> words = {"Apple", "banana", "CHERRY", "DURIAN"};
    
    std::sort(words.begin(), words.end(), caseInsensitiveCompare);
    
    // words: {"Apple", "banana", "CHERRY", "DURIAN"}
    
    return 0;
}
```

In the above code snippet, we define a custom comparison function `caseInsensitiveCompare`, which compares two strings in a case-insensitive manner. We pass this comparison function to `std::sort` to perform the sorting using our custom literal.

## Conclusion

Custom sorting literals in C++ provide a powerful mechanism for sorting objects based on custom criteria or using literals other than the less-than operator. By defining custom sorting predicates or comparison functions, we can tailor the sorting logic to meet our specific requirements.

Understanding and utilizing custom sorting literals can greatly enhance the versatility and flexibility of your C++ programs when dealing with sorting operations.

**References**:
- [C++ Standard Library - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Standard Library - Introsort](https://en.wikipedia.org/wiki/Introsort)