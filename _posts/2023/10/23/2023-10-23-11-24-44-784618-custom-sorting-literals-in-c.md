---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with C++, sorting is a common operation that allows us to arrange elements in a specific order. By default, the `std::sort` function provided by the C++ Standard Library sorts elements using the less-than operator (`<`).

However, there may be cases where we need to sort elements using custom ordering rules. To achieve this, we can define our own sorting literals.

## Defining Custom Sorting Literals

To define custom sorting literals, we can utilize lambda functions in C++. A lambda function is an anonymous function that can be defined inline.

Consider the example where we have a custom class `Person` with member variables `name`, `age`, and `salary`. We want to sort a vector of `Person` objects based on their age.

To create a custom sorting literal based on age, we can define a lambda function that compares two `Person` objects:

```cpp
std::vector<Person> people = { /* initialize vector with Person objects */ };

// Custom sorting literal based on age
std::sort(people.begin(), people.end(), [](const Person& p1, const Person& p2) {
    return p1.age < p2.age;
});
```

In this example, the third argument to `std::sort` is the custom sorting literal. The lambda function takes two `Person` objects `p1` and `p2` as input and compares their ages using the less-than operator (`<`). By returning `true` when `p1.age < p2.age`, the sorting algorithm will sort the vector in ascending order based on age.

## Sorting Criteria

We can extend the example above to sort the vector of `Person` objects based on multiple criteria. For example, sorting by age and then by salary:

```cpp
std::sort(people.begin(), people.end(), [](const Person& p1, const Person& p2) {
    if (p1.age == p2.age) {
        return p1.salary < p2.salary;
    } else {
        return p1.age < p2.age;
    }
});
```

In this case, if two `Person` objects have the same age, we compare their salaries. Otherwise, we compare their ages. By defining the ordering rules within the lambda function, we can easily customize the sorting behavior according to our requirements.

## Conclusion

By using lambda functions, we can define custom sorting literals in C++. This enables us to sort elements based on specific criteria other than the default less-than operator. Custom sorting literals provide flexibility and allow us to organize our data in a way that best suits our needs.

By leveraging lambda functions and `std::sort`, we can create powerful sorting functionality in our C++ applications, ensuring that our data is arranged in the desired order.

# References
- [Lambda Functions in C++](https://en.cppreference.com/w/cpp/language/lambda)
- [std::sort - C++ Reference](https://en.cppreference.com/w/cpp/algorithm/sort)