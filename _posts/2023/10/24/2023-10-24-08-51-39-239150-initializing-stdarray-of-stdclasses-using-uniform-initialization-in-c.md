---
layout: post
title: "Initializing std::array of std::classes using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, you can use the `std::array` container to store a fixed-size collection of objects. One convenient way to initialize an `std::array` is by using uniform initialization syntax. This makes the code more concise and readable.

Uniform initialization allows you to initialize objects using curly braces `{}`. This syntax can also be used to initialize the elements of an `std::array` of `std::classes`.

Consider the following example where we have an `std::array` of `std::string` objects:

```cpp
#include <array>
#include <string>

int main() {
    std::array<std::string, 3> names{"Alice", "Bob", "Charlie"};
    
    // Accessing and printing the elements of the array
    for (const auto& name : names) {
        std::cout << name << std::endl;
    }
    return 0;
}
```

In the above code, we are initializing an `std::array` named `names` of type `std::string` with three elements. The elements are initialized using uniform initialization syntax, where each element is enclosed within curly braces `{}`.

After initializing the `std::array`, we can access and print each element using a range-based for loop.

Output:
```
Alice
Bob
Charlie
```

Uniform initialization also works for more complex classes. Consider the following example where we have an `std::array` of a custom `Person` class:

```cpp
{% raw %}
#include <array>
#include <string>

class Person {
public:
    Person(std::string name, int age) : name_(name), age_(age) {}
    
    std::string getName() const { return name_; }
    int getAge() const { return age_; }
    
private:
    std::string name_;
    int age_;
};

int main() {
    std::array<Person, 2> people{{"Alice", 25}, {"Bob", 30}};
    
    // Accessing and printing the elements of the array
    for (const auto& person : people) {
        std::cout << "Name: " << person.getName() << ", Age: " << person.getAge() << std::endl;
    }
    return 0;
}
{% endraw %}
```

In the above code, we define a `Person` class with a name and age as member variables. The `Person` class has a constructor to initialize these variables. We then create an `std::array` named `people` of type `Person`, and initialize its elements using uniform initialization syntax.

We can access and print the elements of the array using a range-based for loop, and calling the appropriate member functions of the `Person` class.

Output:
```
Name: Alice, Age: 25
Name: Bob, Age: 30
```

Using uniform initialization for initializing `std::array` of `std::classes` helps to make the code more concise, readable, and easily maintainable.