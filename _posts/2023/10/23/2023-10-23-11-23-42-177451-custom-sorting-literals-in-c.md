---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References, Sorting]
comments: true
share: true
---

Sorting is a fundamental operation in programming, and C++ provides various sorting algorithms that work with built-in types. However, when it comes to sorting custom objects or user-defined types, we often need to define our own way of comparing and sorting.

In this article, we will explore how to perform custom sorting in C++ by specifying custom sorting literals. This allows us to define our own rules for comparing and sorting objects based on specific attributes or criteria.

## Defining Custom Sorting Literals

To define custom sorting literals, we need to provide a comparison function or a sorting predicate that will compare two objects and determine their ordering. The comparison function should return `true` if the first object comes before the second object and `false` otherwise.

Let's consider an example where we have a `Person` class with attributes like `name`, `age`, and `height`. We want to sort a collection of `Person` objects based on their age.

```cpp
class Person {
public:
    std::string name;
    int age;
    double height;
};
```

To define a custom sorting literal for the `Person` objects based on their age, we can use a lambda function as follows:

```cpp
std::vector<Person> people;

// Sort based on age in ascending order
std::sort(people.begin(), people.end(), [](const Person& p1, const Person& p2) {
    return p1.age < p2.age;
});
```

In this example, the lambda function takes two `Person` objects `p1` and `p2` as parameters and compares their `age` attributes. It returns `true` if `p1` has a lesser age than `p2`, indicating that `p1` should come before `p2` in the sorted collection.

## Custom Sorting with Class Member Functions

Instead of using lambda functions, we can also define custom sorting literals using class member functions. This approach provides a more modular and reusable way of specifying custom sorting criteria.

Let's modify our `Person` class to include a member function `isOlderThan` that compares the age of two `Person` objects:

```cpp
class Person {
public:
    std::string name;
    int age;
    double height;

    // Compare age with another Person object
    bool isOlderThan(const Person& other) const {
        return age < other.age;
    }
};
```

To perform custom sorting based on the `isOlderThan` member function, we can use the `std::sort` function and provide the member function as a sorting predicate:

```cpp
std::vector<Person> people;

// Sort based on age in ascending order
std::sort(people.begin(), people.end(), &Person::isOlderThan);
```

In this example, the `&Person::isOlderThan` expression references the `isOlderThan` member function of the `Person` class, which will be used for sorting the `Person` objects.

## Conclusion

Custom sorting in C++ allows us to define our own rules for sorting objects based on specific attributes or criteria. By defining custom sorting literals using lambda functions or member functions, we can enhance the flexibility and modularity of sorting operations.

With custom sorting literals, we can sort objects of custom types in any order we desire, making our code more expressive and adaptable.

#References

- [C++ Sort Function - cppreference](https://en.cppreference.com/w/cpp/algorithm/sort)
- [Lambda Functions in C++ - GeeksforGeeks](https://www.geeksforgeeks.org/lambda-expression-in-c/)
- [Member Functions in C++ - GeeksforGeeks](https://www.geeksforgeeks.org/accessing-restricting-inner-members-from-objects-in-c/)

#Hashtags

#C++ #Sorting