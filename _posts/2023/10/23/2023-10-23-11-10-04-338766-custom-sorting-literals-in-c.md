---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [references]
comments: true
share: true
---

Sorting is a common operation in many programming tasks, and C++ provides powerful built-in functions like `std::sort` to easily sort data. However, in some cases, the default sorting mechanism may not be suitable for custom data types or specific sorting requirements. In such scenarios, using custom sorting literals can be a great solution.

## Defining Custom Sorting Criteria

To define custom sorting criteria, you need to provide a function or a lambda expression that compares two elements and returns a boolean value indicating their relative order.

Let's consider an example where we have a `Person` class with attributes `name` and `age`. We want to sort a vector of `Person` objects based on their age in ascending order.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

class Person {
public:
  std::string name;
  int age;
};

int main() {
  std::vector<Person> people = { {"Alice", 25}, {"Bob", 30}, {"Charlie", 20} };

  // Custom sorting criteria based on age
  auto sortByAge = [](const Person& a, const Person& b) {
    return a.age < b.age;
  };

  std::sort(people.begin(), people.end(), sortByAge);

  // Print sorted people
  for (const auto& person : people) {
    std::cout << "Name: " << person.name << ", Age: " << person.age << std::endl;
  }

  return 0;
}
```

In the code above, we define a lambda expression `sortByAge` that compares two `Person` objects based on their age. We pass this lambda expression to `std::sort` as the custom sorting criteria.

## Output

The output of the above code will be:

```
Name: Charlie, Age: 20
Name: Alice, Age: 25
Name: Bob, Age: 30
```

As you can see, the vector of `Person` objects is sorted based on their age in ascending order.

## Conclusion

Custom sorting literals in C++ allow you to sort data using custom criteria that go beyond the default comparators. It gives you flexibility and control over how your data should be sorted. By defining custom sorting criteria using functions or lambda expressions, you can customize the sorting process according to your specific needs.

#references: 
- [C++ Reference - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Reference - Lambdas](https://en.cppreference.com/w/cpp/language/lambda)