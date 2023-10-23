---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

In C++, sorting elements in a collection is a common task. By default, the sorting algorithm uses the less-than (`<`) operator to compare elements. However, in some cases, we may want to define our own custom sorting order. C++ provides a convenient way to achieve this by using *sorting literals*.

## Defining a Custom Sorting Literal

To define a custom sorting literal, we need to define a comparison function that takes two arguments and returns a `bool` value. This function should define the desired sorting order for our elements.

Let's assume we have a `Person` class with `name` and `age` attributes. We want to sort a collection of `Person` objects first by age and then by name.

```cpp
class Person {
public:
    std::string name;
    int age;
};

bool comparePersons(const Person& a, const Person& b) {
    if (a.age == b.age) {
        return a.name < b.name;
    }
    return a.age < b.age;
}
```

The `comparePersons` function compares two `Person` objects based on their age and name attributes. It returns `true` if `a` should be placed before `b` in the sorting order.

## Using Custom Sorting Literals

Once we have the comparison function defined, we can use it with various C++ algorithms that support custom sorting, such as `std::sort` or `std::stable_sort`.

```cpp
{% raw %}
std::vector<Person> people = {{"John", 25}, {"Alice", 30}, {"Bob", 20}};

std::sort(people.begin(), people.end(), comparePersons);

// Output: Bob, John, Alice
for (const auto& person : people) {
    std::cout << person.name << ", ";
}
{% endraw %}
```

In the example above, we create a vector of `Person` objects and sort it using the `comparePersons` function as the sorting literal. The resulting order of elements will be "Bob, John, Alice" because Bob is the youngest, followed by John, and then Alice.

## Conclusion

Custom sorting literals in C++ allow us to define our own sorting order based on specific criteria. By providing a custom comparison function, we can effectively sort elements in a collection according to our desired order. This flexibility enhances the capabilities of the C++ standard library sorting algorithms and enables us to work with various types of data in a customized manner.

#References
- C++ Reference: [std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- C++ Reference: [std::stable_sort](https://en.cppreference.com/w/cpp/algorithm/stable_sort)