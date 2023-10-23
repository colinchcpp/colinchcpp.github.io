---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with arrays or containers in C++, sorting is a common operation. C++ provides the `std::sort` function from the `<algorithm>` library to sort elements in ascending order by default. However, there may be situations where you need to sort elements based on custom criteria or using non-standard data types.

In this blog post, we will explore how to perform custom sorting in C++ using sorting literals. Sorting literals allow you to define your own comparison operators or functions to determine the order of elements during sorting.

## Sorting with Predicates

In C++, a predicate is a function or lambda expression that takes two arguments and returns a boolean value indicating whether the first argument should precede the second argument in the sorted order.

Let's say we have a vector of strings and we want to sort them based on their lengths. We can achieve this by providing a lambda expression as a predicate to the `std::sort` function:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<std::string> strings = {"short", "medium", "very long", "long"};
    
    std::sort(strings.begin(), strings.end(), [](const std::string& a, const std::string& b) {
        return a.size() < b.size();
    });
    
    for (const auto& str : strings) {
        std::cout << str << std::endl;
    }
    
    return 0;
}
```

In this example, the lambda expression compares the sizes of the strings. The `std::sort` function uses this predicate to determine the sorting order.

## Sorting Literal Classes

Sorting literals can also be implemented using classes that provide a custom `operator<` or a `less-than` function. This allows us to define custom sorting logic for user-defined data types.

Suppose we have a class called `Person`, and we want to sort a vector of `Person` objects based on their ages. We can define the custom sorting literal class as follows:

```cpp
class Person {
public:
    Person(const std::string& name, int age)
        : name_(name), age_(age) {}
    
    std::string getName() const {
        return name_;
    }
    
    int getAge() const {
        return age_;
    }
    
private:
    std::string name_;
    int age_;
};

class AgeSortingLiteral {
public:
    bool operator()(const Person& a, const Person& b) const {
        return a.getAge() < b.getAge();
    }
};
```

Now, let's use the `AgeSortingLiteral` class to sort a vector of `Person` objects:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<Person> people = {{"Alice", 28}, {"Bob", 22}, {"Charlie", 35}};
    
    std::sort(people.begin(), people.end(), AgeSortingLiteral());
    
    for (const auto& person : people) {
        std::cout << person.getName() << ", " << person.getAge() << std::endl;
    }
    
    return 0;
}
```

In this example, the `AgeSortingLiteral` class defines the custom sorting logic based on the age of the `Person` objects. The `std::sort` function uses this sorting literal to sort the `people` vector.

## Conclusion

Sorting literals in C++ provide a powerful mechanism to perform custom sorting based on your specific requirements. Whether you need to sort elements based on non-standard data types or define complex sorting criteria, sorting literals allow you to easily customize the sorting process.

By using predicates or implementing custom sorting literal classes, you can extend the capabilities of the `std::sort` function and achieve the desired sorting order in your C++ programs.

# References
- [C++ Reference: std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Reference: Lambda Expressions](https://en.cppreference.com/w/cpp/language/lambda)