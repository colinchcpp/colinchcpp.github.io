---
layout: post
title: "Overloading comparison operators for custom sorting algorithms in C++"
description: " "
date: 2023-09-14
tags: [include, include, cplusplus, sorting, overloading, comparison]
comments: true
share: true
---

Sorting is a fundamental operation in computer science and often requires custom sorting algorithms to achieve specific sorting criteria. In C++, we can implement custom sorting algorithms by overloading comparison operators to define the desired order of elements.

## Comparison Operators in C++

In C++, comparison operators (`<`, `>`, `<=`, `>=`, `==`, `!=`) are used to compare values and determine their relative order. By overloading these operators, we can customize the sorting behavior for our specific needs.

## Overloading the Comparison Operators

To overload comparison operators for custom sorting algorithms, we need to define them as member or non-member functions. Let's consider an example where we want to sort a collection of `Person` objects based on their age.

### Defining the `Person` Class

```cpp
class Person {
public:
    std::string name;
    int age;

    // Constructor
    Person(const std::string& name, int age)
        : name(name), age(age) {}

    // Overload < operator
    bool operator<(const Person& other) const {
        return age < other.age;
    }
};
```

In the above code, we define a `Person` class with `name` and `age` as attributes. We then overload the `<` operator to compare `Person` objects based on their `age` member variable.

### Sorting `Person` Objects

```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<Person> people = {
        {"Alice", 25},
        {"Bob", 19},
        {"Charlie", 30},
        {"David", 22}
    };

    // Sort people based on age
    std::sort(people.begin(), people.end());

    // Print sorted people
    for (const auto& person : people) {
        std::cout << person.name << " (Age: " << person.age << ")\n";
    }

    return 0;
}
```

In the `main` function, we create a vector of `Person` objects and initialize them with names and ages. We then use the `std::sort` function from the `<algorithm>` header to sort the `people` vector using the overloaded `<` operator.

### Result

Running the above code will produce the following output:

```
Bob (Age: 19)
David (Age: 22)
Alice (Age: 25)
Charlie (Age: 30)
```

The `people` vector is sorted in ascending order based on the `age` attribute of each `Person` object.

## Conclusion

By overloading comparison operators, we can customize the sorting behavior for custom sorting algorithms in C++. This allows us to sort objects based on any criteria we define, providing greater flexibility and control over the sorting process.

#cplusplus #sorting #overloading #comparison-operators