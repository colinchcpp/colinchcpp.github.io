---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

Sorting is a common operation in programming, but what if you need to sort elements in a specific order that is not default? In C++, you can achieve this by using custom sorting literals.

## Sorting with Custom Comparison Function

The `std::sort` function in C++ uses a comparison function to determine the order of elements. By default, it uses the less than (`<`) operator to compare elements. However, you can provide a custom comparison function to define your own sorting criteria.

Let's say we have a `Person` class with `name` and `age` attributes. We want to sort a vector of `Person` objects based on their name in alphabetical order. Here's how we can do it:

```cpp
struct Person {
    std::string name;
    int age;
};

// Custom comparison function
bool compareByName(const Person& p1, const Person& p2) {
    return p1.name < p2.name;
}

int main() {
    std::vector<Person> people = {
        {"Alice", 25},
        {"Bob", 30},
        {"Charlie", 20}
    };

    std::sort(people.begin(), people.end(), compareByName);

    for (const Person& person : people) {
        std::cout << person.name << " - Age: " << person.age << std::endl;
    }

    return 0;
}
```

In this example, we define the `compareByName` function as the custom comparison function. It compares two `Person` objects based on their `name` attributes using the less than operator. We then pass this function as the third argument to the `std::sort` function.

Running this code will output the sorted list of people based on their names:

```
Alice - Age: 25
Bob - Age: 30
Charlie - Age: 20
```

## Sorting with Lambda Functions

C++11 introduced lambda functions, which are anonymous functions that can be used inline. They are particularly useful when you want to define a custom comparison function without declaring a separate function.

Using the previous example, we can rewrite the code using a lambda function:

```cpp
int main() {
    std::vector<Person> people = {
        {"Alice", 25},
        {"Bob", 30},
        {"Charlie", 20}
    };

    std::sort(people.begin(), people.end(), [](const Person& p1, const Person& p2) {
        return p1.name < p2.name;
    });

    for (const Person& person : people) {
        std::cout << person.name << " - Age: " << person.age << std::endl;
    }

    return 0;
}
```

The lambda function `[](const Person& p1, const Person& p2)` takes two `Person` objects as parameters and compares them based on their `name` attributes. This inline function is directly passed as the third argument to `std::sort`.

## Conclusion

Custom sorting literals in C++ allow you to sort elements in a specific order that is not default. By providing a custom comparison function or using lambda functions, you can define your own sorting criteria. This flexibility makes it easier to handle various sorting requirements in your C++ programs.

#References
- [C++ std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Lambda Expressions](https://en.cppreference.com/w/cpp/language/lambda)