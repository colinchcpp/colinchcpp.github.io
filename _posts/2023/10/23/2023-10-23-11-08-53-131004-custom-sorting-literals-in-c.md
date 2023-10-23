---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is an essential operation in many programming tasks, and C++ provides a powerful sorting algorithm through the `std::sort` function from the `<algorithm>` library. By default, this function sorts elements using the `<` operator for comparison. However, there are cases where we need to sort objects based on custom criteria or non-standard data types. In such situations, we can define custom sorting literals in C++.

## Defining Custom Sorting Criteria

To define our custom sorting criteria, we can use function objects (functors) or lambda expressions. Let's explore both approaches:

### Using Functors

A functor is an object that can be called like a function. We can define a functor class to encapsulate our custom sorting logic. For example, let's consider a `Person` class with `name` and `age` attributes. We want to sort a collection of `Person` objects by their age. Here's how we can define a functor class for this purpose:

```cpp
class AgeComparator {
public:
    bool operator()(const Person& person1, const Person& person2) {
        return person1.age < person2.age;
    }
};
```

In this example, the `AgeComparator` class defines an `operator()` function that takes two `Person` objects as arguments and compares them based on their ages.

### Using Lambda Expressions

Lambda expressions are inline functions that can be defined directly within other functions or expressions. They provide a concise way to define custom sorting criteria. Let's rewrite the previous example using a lambda expression:

```cpp
auto ageComparator = [](const Person& person1, const Person& person2) {
    return person1.age < person2.age;
};
```

In this example, we define the `ageComparator` lambda expression that takes two `Person` objects and compares their ages.

## Using Custom Sorting Literals

Once we have defined our custom sorting criteria using either functors or lambda expressions, we can use them with the `std::sort` function to sort our objects accordingly. Here's an example of how we can use the `AgeComparator` functor or the `ageComparator` lambda expression to sort a collection of `Person` objects:

```cpp
std::vector<Person> people = { /* collection of Person objects */ };

// Sort using the functor
std::sort(people.begin(), people.end(), AgeComparator());

// Sort using the lambda expression
std::sort(people.begin(), people.end(), ageComparator);
```

In both cases, we pass the custom sorting literal as the third argument to the `std::sort` function. The sort function will then use the provided criteria to order the elements accordingly.

## Conclusion

Custom sorting literals in C++ allow us to define our own sorting criteria for objects or non-standard data types. By utilizing functors or lambda expressions, we can customize the sorting behavior of the `std::sort` function. This flexibility empowers us to handle a wide range of sorting scenarios in our C++ programs.

References:
- [Cppreference - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Functors and Their Uses](https://www.geeksforgeeks.org/functors-in-cpp/)