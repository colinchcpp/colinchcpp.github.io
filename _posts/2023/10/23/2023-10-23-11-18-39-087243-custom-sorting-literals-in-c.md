---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

In C++, the `std::sort` function from the `<algorithm>` library is commonly used to sort elements in a container. By default, `std::sort` uses the less-than (`<`) operator to determine the relative order of elements. However, there may be situations where you want to perform a custom sort based on specific criteria or non-standard sorting rules.

In such cases, you can provide a custom sorting predicate to `std::sort`. A sorting predicate is a function or lambda expression that defines the order of elements during the sorting process. This allows you to define your own sorting rules or criteria.

## Sorting Based on Custom Rules

Let's say we want to sort a vector of strings based on the length of the strings. By default, `std::sort` will sort the strings alphabetically. However, we can define our custom sorting rule by creating a lambda function that compares the lengths of the strings:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>

int main() {
    std::vector<std::string> words = {"apple", "banana", "car", "dog", "elephant"};

    std::sort(words.begin(), words.end(), [](const std::string& a, const std::string& b) {
        return a.length() < b.length();
    });

    for (const auto& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

In the above code, we define a lambda function as the last argument to `std::sort`. The lambda takes two `const std::string&` references, `a` and `b`, which represent two elements being compared. The lambda returns `true` if `a` should appear before `b` in the sorted sequence.

In this case, the lambda function compares the lengths of the strings (`a.length() < b.length()`) and sorts them in ascending order based on length. The sorted result is printed to the console.

## Sorting Based on Enumerated Values

Another common scenario is sorting based on enumerated values rather than the values themselves. For example, suppose you have an enum type representing different priorities of tasks, and you want to sort a vector of tasks based on their priority level.

In C++, enums are represented as integral types. You can create a custom sorting predicate that compares the enum values and defines the desired order:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

enum class Priority {
    Low,
    Medium,
    High
};

struct Task {
    std::string name;
    Priority priority;
};

int main() {
    std::vector<Task> tasks = {
        {"Task 1", Priority::Medium},
        {"Task 2", Priority::Low},
        {"Task 3", Priority::High},
        {"Task 4", Priority::Medium}
    };
    
    std::sort(tasks.begin(), tasks.end(), [](const Task& a, const Task& b) {
        return static_cast<int>(a.priority) < static_cast<int>(b.priority);
    });

    for (const auto& task : tasks) {
        std::cout << task.name << " ";
    }

    return 0;
}
```

In the above code, we have an enum `Priority` representing low, medium, and high priority levels. We also have a struct `Task` that consists of a task name and its priority.

We define a lambda function as the sorting predicate, comparing the priority values using the static_cast to `int`. The tasks are then sorted based on their priority levels in ascending order.

## Conclusion

Custom sorting literals in C++ allow you to define your own sorting rules based on specific criteria. By providing a custom sorting predicate to `std::sort`, you can sort elements in a container based on non-standard rules, such as length, enumerated values, or any other custom logic. This gives you flexibility and control over the sorting process in your C++ programs.

#References:
- [cppreference.com - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [cplusplus.com - Sorting elements](http://www.cplusplus.com/doc/oldtutorial/templates/)
- [GeeksforGeeks - Sorting a Vector in C++](https://www.geeksforgeeks.org/sort-vector-c/)