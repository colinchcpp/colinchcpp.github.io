---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In C++, sorting elements in a container like an array or a vector is a common task. By default, the C++ standard library provides sorting algorithms that work well for built-in types like integers or floats. However, when dealing with custom objects or user-defined types, the default sorting may not produce the desired results.

To achieve custom sorting, you can define your own comparison function or use lambda expressions. This allows you to define how elements should be sorted based on specific criteria.

Let's say we have a class called `Person`, which has two attributes - `name` and `age`. We want to sort a vector of `Person` objects based on their age.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

class Person {
public:
    std::string name;
    int age;
    
    Person(std::string name, int age) : name(name), age(age) {}
};

bool compareByAge(const Person& p1, const Person& p2) {
    return p1.age < p2.age;
}

int main() {
    std::vector<Person> people;
    people.push_back(Person("John", 25));
    people.push_back(Person("Emily", 30));
    people.push_back(Person("Adam", 20));

    // Sort based on age using compareByAge function
    std::sort(people.begin(), people.end(), compareByAge);

    // Print sorted list
    for (const auto& person : people) {
        std::cout << person.name << ", " << person.age << std::endl;
    }
    return 0;
}
```

In the code above, we define a comparison function `compareByAge` that takes two `Person` objects as parameters and returns `true` if the age of the first person is less than the age of the second person. This function acts as a custom sorting criterion.

We then use the `std::sort` algorithm function to sort the `people` vector based on the defined comparison function. Finally, we print the sorted list, which will be displayed in ascending order of age.

You can also achieve the same result using a lambda expression, which provides a concise way of defining small inline functions. The lambda expression can be passed directly as the third argument to `std::sort`:

```cpp
std::sort(people.begin(), people.end(), [](const Person& p1, const Person& p2) {
    return p1.age < p2.age;
});
```

By defining a custom comparison function or using a lambda expression, you can sort your custom objects or user-defined types based on any criteria you desire. This allows for flexible and customizable sorting in C++.