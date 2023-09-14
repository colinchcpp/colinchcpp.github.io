---
layout: post
title: "Overloading comparison operators in C++ for custom types"
description: " "
date: 2023-09-14
tags: [operators]
comments: true
share: true
---

When working with custom types in C++, it is often necessary to define how comparison operations, such as equality or less than, should be performed. By overloading comparison operators, we can provide custom implementations to compare instances of our custom types.

To overload a comparison operator, we need to define a member function or a friend function that corresponds to the desired operator. The following examples demonstrate how to overload the equality (`==`) and less than (`<`) operators for a custom `Person` class:

```cpp
class Person {
public:
    Person(const std::string& name, int age)
        : name_(name), age_(age) {}

    bool operator==(const Person& other) const {
        return (name_ == other.name_) && (age_ == other.age_);
    }

    bool operator<(const Person& other) const {
        if (name_ == other.name_) {
            return age_ < other.age_;
        }
        return name_ < other.name_;
    }

private:
    std::string name_;
    int age_;
};
```

In this example, the `Person` class has a name and an age. The `operator==` compares two `Person` objects by checking if their names and ages are equal. The `operator<` compares `Person` objects first by name and then by age.

Once the operators are overloaded, we can use them to compare instances of the `Person` class. Here's an example of how we can use these overloaded operators:

```cpp
Person p1("John", 25);
Person p2("Jane", 30);
Person p3("John", 25);

if (p1 == p2) {
    // Do something if p1 and p2 are equal
}

if (p1 < p2) {
    // Do something if p1 is less than p2
}

if (p1 == p3) {
    // This condition will be true, as p1 and p3 have the same name and age
}
```

By overloading these comparison operators, we can customize the behavior of comparison operations for our custom types. This allows us to compare instances based on specific criteria defined by our application.

## Conclusion

Overloading comparison operators in C++ for custom types allows us to define how instances of our custom classes should be compared. By providing custom implementations for equality and less than operators, we can make our code more expressive and intuitive. By following the examples above, you can now successfully overload comparison operators for your own custom types in C++.

#cpp #operators #C++