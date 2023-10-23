---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [Sorting]
comments: true
share: true
---

In many cases, the default sorting order provided by C++ may not meet our specific requirements. Fortunately, C++ allows us to define our own sorting criteria by using custom sorting literals. In this blog post, we will explore how to implement custom sorting literals in C++.

### What are Sorting Literals?

Sorting literals are special functions or operators that define the order in which elements should be sorted. By default, C++ uses the less-than operator (`<`) to sort elements in ascending order. However, in some cases, we may want to sort elements based on a custom logic or criteria.

### Defining Custom Sorting Criteria

To define a custom sorting criteria, we need to provide a function or operator that compares two elements and returns a boolean value indicating their order. The function or operator should return `true` if the first element should come before the second, and `false` otherwise.

Let's consider an example where we have a `Person` class with two member variables: `name` and `age`. We want to sort a collection of `Person` objects based on their age in descending order. To achieve this, we need to define a custom sorting literal.

```cpp
class Person {
  string name;
  int age;
public:
  Person(string n, int a) : name(n), age(a) {}
  int getAge() const { return age; }
};

bool operator<(const Person& p1, const Person& p2) {
  return p1.getAge() > p2.getAge();
}
```

In the above code, we define the `<` operator for comparing two `Person` objects. We use the `getAge()` method to compare the ages of two persons, and return `true` if the age of the first person is greater than the second person.

### Using Custom Sorting Literals

To use the custom sorting literal, we simply pass it as a parameter to the `std::sort` function from the C++ standard library. The `std::sort` function will use the provided sorting literal to sort the elements accordingly.

```cpp
int main() {
  vector<Person> persons;
  persons.push_back(Person("Alice", 25));
  persons.push_back(Person("Bob", 30));
  persons.push_back(Person("Charlie", 20));
  
  std::sort(persons.begin(), persons.end());
  
  for(const auto& person : persons) {
    cout << person.getAge() << " ";
  }
  
  return 0;
}
```

In the above code, we create a vector of `Person` objects and populate it with three persons having different ages. We then call `std::sort` with the `persons.begin()` and `persons.end()` iterators, which sorts the vector based on the custom sorting literal we defined earlier.

### Conclusion

Custom sorting literals provide a flexible way to define our own sorting criteria in C++. By defining special functions or operators, we can sort elements based on any custom logic. This allows us to have more control over how our data is sorted and enables us to implement complex sorting algorithms if needed.

**#C++ #Sorting**