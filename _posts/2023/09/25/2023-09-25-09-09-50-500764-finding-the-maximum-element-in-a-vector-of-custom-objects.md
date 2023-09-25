---
layout: post
title: "Finding the maximum element in a vector of custom objects"
description: " "
date: 2023-09-25
tags: [programming]
comments: true
share: true
---

When working with a vector of custom objects in C++, you may sometimes need to find the maximum element based on a specific attribute or property of the objects. In this blog post, we'll explore different approaches to accomplish this task efficiently.

## Method 1: Using a Custom Comparator

One way to find the maximum element is by using a custom comparator function or lambda expression. This approach gives you flexibility in determining the criteria for comparison.

### Example Code

```cpp
struct Person {
    std::string name;
    int age;

    Person(std::string name, int age)
        : name(name), age(age) {
    }
};

// Custom comparator function to compare persons based on age
bool personComparator(const Person& p1, const Person& p2) {
    return p1.age < p2.age;
}

int main() {
    std::vector<Person> persons = {
        {"Alice", 25},
        {"Bob", 30},
        {"Charlie", 20}
    };

    // Find the maximum element using custom comparator
    auto maxPerson = *std::max_element(persons.begin(), persons.end(), personComparator);

    std::cout << "Max person: " << maxPerson.name << " (" << maxPerson.age << ")" << std::endl;

    return 0;
}
```

### Output

```
Max person: Bob (30)
```

## Method 2: Using a Member Function Pointer

Another approach is to use a member function pointer to access the desired property of the objects for comparison. This simplifies the comparison process and makes it more concise.

### Example Code

```cpp
struct Person {
    std::string name;
    int age;

    Person(std::string name, int age)
        : name(name), age(age) {
    }

    // Member function pointer to access the age property
    static int ageGetter(const Person& person) {
        return person.age;
    }
};

int main() {
    std::vector<Person> persons = {
        {"Alice", 25},
        {"Bob", 30},
        {"Charlie", 20}
    };

    // Find the maximum element using a member function pointer
    auto maxPerson = *std::max_element(persons.begin(), persons.end(), [](const Person& p1, const Person& p2) {
        return Person::ageGetter(p1) < Person::ageGetter(p2);
    });

    std::cout << "Max person: " << maxPerson.name << " (" << maxPerson.age << ")" << std::endl;

    return 0;
}
```

### Output

```
Max person: Bob (30)
```

## Conclusion

Finding the maximum element in a vector of custom objects can be achieved using various techniques. In this blog post, we explored two methods: using a custom comparator and using a member function pointer.

You can choose the method that suits your specific requirements. The first method gives you more control over the comparison criteria, while the second method provides a more concise syntax.

#programming #C++