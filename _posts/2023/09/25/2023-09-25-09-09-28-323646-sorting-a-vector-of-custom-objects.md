---
layout: post
title: "Sorting a vector of custom objects"
description: " "
date: 2023-09-25
tags: [SortingVectors]
comments: true
share: true
---

To begin with, let's create a simple custom object called `Person` with two properties: `name` and `age`.

```cpp
struct Person {
    std::string name;
    int age;
};
```

Now, let's assume that we have a vector of `Person` objects called `people`. We want to sort this vector based on the `age` property in ascending order. To achieve this, we can use the `std::sort` function from the C++ standard library.

```cpp
{% raw %}
std::vector<Person> people = {{"Alice", 25}, {"Bob", 30}, {"Charlie", 20}};

std::sort(people.begin(), people.end(), [](const Person& a, const Person& b) {
    return a.age < b.age;
});
{% endraw %}
```

In the code above, we pass a lambda function as the third argument to `std::sort`. This lambda function compares two `Person` objects based on their `age` property and returns `true` if the first object should come before the second object in the sorted sequence.

If we want to sort the vector in descending order, we can modify the lambda function to use the greater than (`>`) operator instead.

```cpp
std::sort(people.begin(), people.end(), [](const Person& a, const Person& b) {
    return a.age > b.age;
});
```

In addition to sorting by a single property, we can also sort by multiple properties. For example, let's sort the `people` vector first by `age` in ascending order, and then by `name` in descending order.

```cpp
std::sort(people.begin(), people.end(), [](const Person& a, const Person& b) {
    if (a.age == b.age) {
        return a.name > b.name;
    }
    return a.age < b.age;
});
```

By adjusting the conditions in the lambda function, we can specify the custom sorting criteria based on the properties of the custom object.

In conclusion, sorting a vector of custom objects in C++ can be achieved by using the `std::sort` function along with a lambda function for custom comparison. By manipulating the conditions within the lambda function, we can define the sorting behavior based on the properties of the custom object.

#C++ #SortingVectors