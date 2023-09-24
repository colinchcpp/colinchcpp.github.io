---
layout: post
title: "Custom comparison functions with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [programming, smartpointers]
comments: true
share: true
---

When working with smart pointers like `std::unique_ptr` and `std::shared_ptr` in C++, you might encounter situations where you need to compare them using custom criteria. While these smart pointers provide their own default comparison behavior, you can customize it to fit your specific needs.

In this blog post, we'll explore how to define custom comparison functions for `std::unique_ptr` and `std::shared_ptr` and discuss some common use cases where this technique can be useful.

## Comparing std::unique_ptr

`std::unique_ptr` is a smart pointer that represents ownership of a dynamically allocated object and ensures its deletion when it goes out of scope. By default, `std::unique_ptr` uses the equality operator (`==`) to compare two instances. However, if the underlying object does not provide an appropriate `operator==`, you will need to define a custom comparison function.

Here's an example of a custom comparison function for `std::unique_ptr` that compares the values of two `int` pointers:

```cpp
bool compare_unique_ptr(const std::unique_ptr<int>& a, const std::unique_ptr<int>& b) {
    return *a == *b;
}
```

### Common use case with std::unique_ptr

One common use case for custom comparison functions with `std::unique_ptr` is when you have a container (such as `std::set` or `std::unordered_set`) that needs to store unique pointers and use a specific comparison criterion other than the default one. By providing a custom comparison function, you can define your own way of comparing the objects pointed to by the unique pointers.

## Comparing std::shared_ptr

`std::shared_ptr` is a smart pointer that represents shared ownership of a dynamically allocated object. Similar to `std::unique_ptr`, `std::shared_ptr` uses the equality operator by default for comparison. However, in cases where you need to use custom criteria, you can define a custom comparison function as well.

Let's consider an example where you have a `Person` class and you want to compare two `std::shared_ptr<Person>` instances based on their age:

```cpp
struct Person {
    std::string name;
    int age;

    Person(const std::string& n, int a) : name(n), age(a) {}
};

// Custom comparison function
bool compare_shared_ptr(const std::shared_ptr<Person>& a, const std::shared_ptr<Person>& b) {
    return a->age < b->age;
}
```

### Common use case with std::shared_ptr

A common use case for custom comparison functions with `std::shared_ptr` is when you need to sort a collection of shared pointers based on a specific criteria. By providing a custom comparison function, you can define the sorting order based on any member variable or any other criterion of the underlying object.

## Conclusion

Custom comparison functions come in handy when you need to compare `std::unique_ptr` and `std::shared_ptr` instances using custom criteria. By defining your own comparison functions, you can tailor the comparison behavior to suit your specific needs.

Remember to consider the use cases mentioned in this blog post and adapt the code examples accordingly to fit your requirements.

#programming #smartpointers