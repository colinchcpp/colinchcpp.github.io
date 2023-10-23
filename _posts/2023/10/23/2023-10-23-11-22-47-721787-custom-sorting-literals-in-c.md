---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When sorting elements in C++, the default behavior is to compare them using their built-in comparison operators. However, in some cases, you may want to sort elements using a custom order or specific criteria. This can be achieved by providing a custom sorting literal.

A sorting literal is a function or functor used to define the comparison logic for sorting elements. It takes two elements and returns a boolean value indicating whether the first element should come before the second element in the sorted order.

Let's see an example of how to use custom sorting literals in C++.

## Creating a Custom Sorting Literal

To create a custom sorting literal, you need to define a function or functor that implements the comparison logic. Let's say we have a class `Person` with `name` and `age` attributes, and we want to sort a vector of `Person` objects based on their age.

```cpp
struct Person {
    std::string name;
    int age;
};

// Custom sorting literal for sorting Person objects based on age
bool sortByAge(const Person& p1, const Person& p2) {
    return p1.age < p2.age;
}
```

In this example, the `sortByAge` function takes two `Person` objects as arguments and compares their ages. It returns `true` if the age of the first person is less than the age of the second person, indicating that the first person should come before the second person in the sorted order.

## Using the Custom Sorting Literal

To use the custom sorting literal in the sorting algorithm, you need to pass it as the third argument to the `std::sort` function or any other sorting function that accepts a custom comparison function.

```cpp
std::vector<Person> people = {{"Alice", 25}, {"Bob", 30}, {"Charlie", 20}};
std::sort(people.begin(), people.end(), sortByAge);
```

In this example, we have a vector of `Person` objects `people` that we want to sort based on their age. We pass the `sortByAge` sorting literal as the third argument to the `std::sort` function.

After sorting, the `people` vector will be rearranged in ascending order of age. The output will be:

```
Charlie, 20
Alice, 25
Bob, 30
```

## Custom Sorting Literals with Lambda Functions

Instead of defining a separate function or functor for each sorting literal, you can use lambda functions. Lambda functions provide a concise way to define temporary functions inline.

Using the same example, we can rewrite the custom sorting literal using a lambda function:

```cpp
std::sort(people.begin(), people.end(), [](const Person& p1, const Person& p2) {
    return p1.age < p2.age;
});
```

In this case, the sorting literal is defined directly inside the `std::sort` function call using the lambda function syntax `[](const Person& p1, const Person& p2) { /* comparison logic */ }`.

Using lambda functions for custom sorting literals can make the code more readable and compact, especially for simple sorting criteria.

## Conclusion

Custom sorting literals in C++ allow you to define your own sorting criteria for elements. This gives you the flexibility to sort elements based on custom orders or specific attributes. You can create custom sorting literals using functions or lambda functions and pass them as arguments to sorting algorithms.

By leveraging custom sorting literals, you can tailor the sorting behavior of your C++ code to meet specific requirements.