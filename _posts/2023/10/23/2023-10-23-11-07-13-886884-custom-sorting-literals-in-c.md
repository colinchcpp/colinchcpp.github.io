---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with sorting algorithms in C++, you may often come across the need to perform custom sorting based on specific criteria. The standard sorting functions provided by the C++ Standard Library, such as `std::sort`, primarily perform sorting based on the natural order of the elements. However, in some cases, you may require a different sorting order based on custom rules or literals. In this blog post, we will explore how to perform custom sorting literals in C++.

## Defining Custom Sorting Criteria

To achieve custom sorting in C++, you need to define a sorting criteria that will determine the order in which elements should be sorted. This can be done by creating a comparison function or a lambda expression.

### Using a Comparison Function

A comparison function is a user-defined function that takes two elements as input and returns a boolean value indicating whether the first element should come before the second in the sorted order. Let's consider an example where we want to sort a vector of strings based on the length of the strings.

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>

bool compareByLength(const std::string& a, const std::string& b) {
    return a.length() < b.length();
}

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};
    
    std::sort(words.begin(), words.end(), compareByLength);
    
    for (const std::string& word : words) {
        std::cout << word << " ";
    }
    
    return 0;
}
```

In the above code, we define a custom comparison function `compareByLength` that compares two strings based on their length.

### Using a Lambda Expression

Alternatively, we can use a lambda expression to define the custom sorting criteria inline. Let's rewrite the previous example using a lambda expression.

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};
    
    std::sort(words.begin(), words.end(), [](const std::string& a, const std::string& b) {
        return a.length() < b.length();
    });
    
    for (const std::string& word : words) {
        std::cout << word << " ";
    }
    
    return 0;
}
```

In this code, we define the sorting criteria directly within the `std::sort` function call using a lambda expression.

## Custom Sorting with User-Defined Objects

In addition to sorting based on literals or attributes of built-in data types, you can also perform custom sorting on user-defined objects. This can be achieved by overloading the `<` operator in the object's class definition.

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

class Person {
public:
    Person(const std::string& name, int age)
        : name(name), age(age) {}
    
    std::string getName() const {
        return name;
    }
    
    int getAge() const {
        return age;
    }
    
    bool operator<(const Person& other) const {
        return age < other.age;
    }
    
private:
    std::string name;
    int age;
};

int main() {
    std::vector<Person> people = {{"Alice", 25}, {"Bob", 20}, {"Charlie", 30}};
    
    std::sort(people.begin(), people.end());
    
    for (const Person& person : people) {
        std::cout << person.getName() << " (" << person.getAge() << ") ";
    }
    
    return 0;
}
```

In the above code, we define a `Person` class with a custom `<` operator overload that compares people based on their age.

By providing a custom sorting criteria through comparison functions, lambda expressions, or operator overloading, you can accomplish custom sorting in C++ based on your specific requirements.

## Conclusion

Performing custom sorting literals in C++ allows you to sort elements based on more complex criteria than the default natural order. By defining custom comparison functions or lambda expressions, you can achieve the desired sorting order. Additionally, with operator overloading, you can perform custom sorting on user-defined objects.