---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [cplusplus, sorting]
comments: true
share: true
---

When working with sorting algorithms in C++, sometimes we encounter situations where we need to define our own custom sorting order for specific data types or structures. In such cases, it becomes essential to implement custom sorting literals. 

## Sorting Literals in C++

Sorting literals are the values that define the order in which elements should be sorted. By default, C++ uses the default sorting order of the data type being sorted, such as numerical order for integers or lexicographical order for strings. However, in some scenarios, this default order may not meet our requirements.

To define a custom sorting order, we need to provide a comparison function or a functor (function object) that defines the ordering logic for the given data type. 

## Defining Custom Sorting Order

Here's an example of how we can define a custom sorting order for a struct called `Person` with two members: `name` and `age`.

```c++
struct Person {
    std::string name;
    int age;
};

bool comparePersons(const Person& p1, const Person& p2) {
    // Compare based on age, then name
    if (p1.age != p2.age) {
        return p1.age < p2.age;
    } else {
        return p1.name < p2.name;
    }
}
```

In the above code, we define a function `comparePersons()` to compare two instances of the `Person` struct. The function compares the `age` first and if they are equal, it compares the `name` using the `<` operator. This comparison function serves as our custom sorting literal.

## Using Custom Sorting Literals

Once we have defined our custom sorting literal, we can simply pass it as a parameter to the sorting function, such as `std::sort` in C++ Standard Library, to achieve the desired sorting order. 

```c++
std::vector<Person> people = { /* ... */ };

std::sort(people.begin(), people.end(), comparePersons);
```

In the code above, `comparePersons` is passed as the third argument to `std::sort`. This instructs the sorting algorithm to use our custom sorting literal when ordering the elements in the `people` vector.

## Conclusion

Custom sorting literals in C++ allow us to define our own sorting order for specific data types or structures. By providing a comparison function or functor, we can customize the sorting algorithm to meet our requirements. By utilizing custom sorting literals, we can achieve greater flexibility and control over the sorting process in our C++ programs.

_references:_
- [std::sort - C++ Reference](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Comparison-based Sorting - GeeksforGeeks](https://www.geeksforgeeks.org/c-comparison-based-sorting/) 

## #cplusplus #sorting