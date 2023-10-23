---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is a fundamental operation in programming, allowing us to efficiently organize data in ascending or descending order. In many cases, the default sorting behavior is sufficient, but there are times when we need to customize the sorting order based on specific criteria.

In C++, the standard library provides a versatile sorting algorithm called `std::sort()`, which can be customized using custom sorting literals. Custom sorting literals allow us to define our own ordering rules for elements in a collection.

## Custom Sorting with Comparison Function

The simplest way to customize the sorting order is by providing a custom comparison function. The comparison function should take two arguments and return `true` if the first element should appear before the second element in the sorted order.

Let's consider an example where we have a collection of `Person` objects and we want to sort them based on their age in descending order:

```cpp
struct Person {
    std::string name;
    int age;
};

bool compareByAgeDescending(const Person& a, const Person& b) {
    return a.age > b.age;
}

int main() {
    std::vector<Person> people = { 
        { "John", 30 },
        { "Alice", 25 },
        { "Bob", 35 }
    };

    std::sort(people.begin(), people.end(), compareByAgeDescending);

    for (const auto& person : people) {
        std::cout << person.name << " (" << person.age << ")\n";
    }

    return 0;
}
```

The `compareByAgeDescending` function is passed as the third argument to `std::sort()` to define the custom sorting order based on age. Running this code will output:

```
Bob (35)
John (30)
Alice (25)
```

## Custom Sorting with Lambda Function

C++11 introduced lambda functions, which provide a concise way to define anonymous functions inline. We can use lambda functions to define custom sorting order without explicitly defining a separate comparison function.

Let's modify our previous example to use a lambda function for custom sorting:

```cpp
std::sort(people.begin(), people.end(), [](const Person& a, const Person& b) {
    return a.age > b.age; // Sort by age descending
});
```

Using lambda functions, the code becomes more compact and readable.

## Conclusion

Custom sorting literals in C++ offer flexibility when it comes to sorting elements in a collection based on custom criteria. By providing a custom comparison function or using lambda functions, we can easily define our own sorting order. This powerful feature allows us to sort elements in any desired order, making our code more expressive and flexible.

By utilizing custom sorting literals, we can empower our C++ programs to efficiently handle complex sorting scenarios.