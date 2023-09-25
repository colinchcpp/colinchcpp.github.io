---
layout: post
title: "Finding the index of a specific object in a vector of custom objects"
description: " "
date: 2023-09-25
tags: [vector, custom]
comments: true
share: true
---
title: Finding the Index of a Specific Object in a Vector of Custom Objects
description: Learn how to find the index of a specific object in a vector of custom objects in C++.
tags: #C++ #vector #custom-objects
---

When working with vectors in C++, there may come a situation where you need to find the index of a specific object within the vector. This can be especially useful when you have a vector containing multiple instances of custom objects and you want to locate a particular object quickly. In this blog post, we will explore how to find the index of a specific object in a vector of custom objects.

Let's assume that we have a custom class called `Person` with properties such as `name` and `age`. We have a vector of `Person` objects named `peopleVector`. Now, we want to find the index of a specific `Person` object in this vector.

Here's an example code snippet that demonstrates how to accomplish this task:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

class Person {
public:
    std::string name;
    int age;
    // Constructors, getters, setters, etc.
};

int main() {
    std::vector<Person> peopleVector;

    // Populate the vector with some Person objects
    peopleVector.push_back(Person{"John", 25});
    peopleVector.push_back(Person{"Alice", 30});
    peopleVector.push_back(Person{"Bob", 35});

    Person targetPerson{"Alice", 30};

    auto iter = std::find(peopleVector.begin(), peopleVector.end(), targetPerson);
    if (iter != peopleVector.end()) {
        // The element was found
        int index = std::distance(peopleVector.begin(), iter);
        std::cout << "Index of targetPerson: " << index << std::endl;
    } else {
        // The element was not found
        std::cout << "Target person not found in vector!" << std::endl;
    }

    return 0;
}
```

In this code, we create a `Person` object named `targetPerson` which we want to locate in the `peopleVector`. We use the `std::find` algorithm from the `<algorithm>` library to search for the object. If the object is found, we calculate the index using `std::distance` and output it. Otherwise, we display a message indicating that the target person was not found in the vector.

By using `std::find` and `std::distance`, we can efficiently find the index of a specific object in a vector of custom objects in C++. This approach allows us to quickly locate desired objects within a vector, enabling us to perform further operations or retrieve additional information associated with the object.

So, next time you need to find the index of a specific object in a vector of custom objects, remember this simple technique and save yourself some time and effort!

#C++ #vector #custom-objects