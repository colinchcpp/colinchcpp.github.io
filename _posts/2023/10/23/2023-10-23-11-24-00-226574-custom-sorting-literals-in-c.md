---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

In C++, sorting a collection of objects usually involves using the `std::sort` function from the `<algorithm>` library. By default, `std::sort` applies the less-than operator (`<`) to compare and sort the elements. However, if you need to perform a custom sorting logic using non-standard comparison criteria, you can use custom sorting literals.

## Sorting with custom literals

Custom sorting literals allow you to define your own comparison logic when sorting objects. It is particularly useful when sorting objects based on properties that do not have a built-in comparison operator.

To define a custom sorting literal, you need to overload the less-than operator (`<`) for your object or create a comparison function that takes two objects and returns the desired ordering.

Let's take an example where we have a `Person` class with `name` and `age` properties. We want to sort a collection of `Person` objects first by name and then by age.

```cpp
class Person {
public:
    std::string name;
    int age;

    Person(const std::string& name, int age) : name(name), age(age) {}

    bool operator<(const Person& other) const {
        if (name < other.name) {
            return true;
        } else if (name == other.name) {
            return age < other.age;
        }
        return false;
    }
};

int main() {
    std::vector<Person> people = {
        Person("John", 25),
        Person("Alice", 30),
        Person("Alice", 25),
        Person("Bob", 20)
    };

    std::sort(people.begin(), people.end());

    for (const auto& person : people) {
        std::cout << person.name << ", " << person.age << std::endl;
    }

    return 0;
}
```

In the `Person` class, we have overloaded the less-than operator to first compare the `name` property and then the `age` property. The `std::sort` function will use this custom ordering when sorting the `people` vector.

## Output

```
Alice, 25
Alice, 30
Bob, 20
John, 25
```

As seen in the output, the `people` vector is sorted based on the custom sorting logic defined in the `Person` class.

## Conclusion

Custom sorting literals provide a convenient way to define and use non-standard comparison logic when sorting objects in C++. By overloading the less-than operator or providing a custom comparison function, you can ensure that your objects are sorted according to your specific requirements.

#References
- [std::sort - C++ Reference](https://en.cppreference.com/w/cpp/algorithm/sort)
- [std::less - C++ Reference](https://en.cppreference.com/w/cpp/utility/functional/less)