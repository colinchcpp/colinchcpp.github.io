---
layout: post
title: "Initializing std::array of std::structs using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Let's say we have a struct `Person` with two members: `name` and `age`.

```cpp
#include <array>
#include <string>

struct Person {
    std::string name;
    int age;
};

int main() {
    std::array<Person, 3> people = {
        {"Alice", 25},
        {"Bob", 30},
        {"Charlie", 35}
    };
    
    // Accessing the elements in the array
    for (const auto& person : people) {
        std::cout << "Name: " << person.name << ", Age: " << person.age << std::endl;
    }

    return 0;
}
```

In this example, we are creating a `std::array` called `people` of size 3, where each element is of type `Person`. We initialize the array using uniform initialization syntax by providing a list of elements enclosed in curly braces `{}`.
Each element is itself initialized using a braced-init-list `{}` containing the values for `name` and `age`.

The code then demonstrates how to access the elements in the array using a range-based `for` loop. It prints the name and age of each person.

Executing the above code will output:

```
Name: Alice, Age: 25
Name: Bob, Age: 30
Name: Charlie, Age: 35
```

Uniform initialization simplifies the initialization process and provides a more readable and consistent way to initialize arrays of structs in C++. It is available in C++11 and later versions.

References:
- [std::array - cppreference.com](https://en.cppreference.com/w/cpp/container/array)
- [Uniform initialization - cppreference.com](https://en.cppreference.com/w/cpp/language/list_initialization)