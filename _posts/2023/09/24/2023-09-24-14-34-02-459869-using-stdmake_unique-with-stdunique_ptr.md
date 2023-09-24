---
layout: post
title: "Using `std::make_unique` with `std::unique_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

In modern C++, `std::unique_ptr` is commonly used for managing dynamic memory allocation. It ensures proper resource ownership and automatic resource cleanup. To create and initialize a `std::unique_ptr`, the recommended approach is to use `std::make_unique`, which simplifies memory allocation and reduces the risk of memory leaks.

## What is `std::make_unique`?

`std::make_unique` is a C++14 addition that provides a convenient way to create a `std::unique_ptr` and initialize it with an object. It follows the same principles as `std::make_shared` for `std::shared_ptr`.

## How does `std::make_unique` work?

The `std::make_unique` function takes the desired object's type and parameters as arguments and returns a newly created `std::unique_ptr` pointing to the object. It internally uses the `new` operator to allocate memory and construct the object.

## Advantages of using `std::make_unique`

Using `std::make_unique` has several advantages over manually creating a `std::unique_ptr`:

1. **Safety**: `std::make_unique` ensures proper exception safety by automatically cleaning up memory in case of an exception.
2. **Clarity**: It enhances code readability by clearly indicating ownership and simplifying memory allocation and object initialization in a single line.
3. **Avoiding memory leaks**: Since `std::unique_ptr` automatically deallocates memory when it goes out of scope, using `std::make_unique` reduces the risk of forgetting to deallocate memory.

## Example usage of `std::make_unique`

Let's consider an example where we want to create a `std::unique_ptr` to manage a dynamically allocated `Person` object:

```cpp
#include <memory>
#include <string>

struct Person {
    std::string name;
    int age;
};

int main() {
    auto person = std::make_unique<Person>("John Doe", 30);

    // Accessing object attributes
    std::cout << "Name: " << person->name << ", Age: " << person->age << std::endl;

    return 0;
}
```
In the code snippet above, we use `std::make_unique` to create a `std::unique_ptr` named `person`, which points to a dynamically allocated `Person` object. We pass the constructor arguments `"John Doe"` and `30` to initialize the object. By doing so, we ensure proper memory management and easy access to object attributes.

## Conclusion

Using `std::make_unique` simplifies memory allocation and initialization of `std::unique_ptr` objects, resulting in safer and cleaner code. Make sure to familiarize yourself with the `std::make_unique` function to leverage its benefits when working with dynamic memory allocation in C++.

#cpp #memory-management