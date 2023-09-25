---
layout: post
title: "Counting occurrences of a specific attribute in a 2D vector of custom objects"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

When working with a 2D vector of custom objects, it might be necessary to count the occurrences of a specific attribute across all objects in the vector. This can be useful in scenarios where you need to analyze or manipulate data based on the frequency of a certain attribute.

Here's an example scenario: let's say we have a 2D vector `myVector` of `Person` objects, and each `Person` object has an attribute `age`. We want to count how many times each age appears in the vector.

To accomplish this, we can use a `std::map` to store the counts for each age value. The `std::map` will associate each age with its occurrence count.

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <map>

struct Person {
    std::string name;
    int age;
};

int main() {
    std::vector<std::vector<Person>> myVector = {
        {{ "Alice", 20 }, { "Bob", 30 }, { "Charlie", 20 }},
        {{ "Dave", 25 }, { "Eve", 30 }, { "Frank", 30 }},
        {{ "Grace", 20 }, { "Henry", 25 }}
    };

    std::map<int, int> ageCount; // Map to store age counts

    for (const auto& row : myVector) {
        for (const auto& person : row) {
            ageCount[person.age]++; // Increment count for each age
        }
    }

    // Display the counts
    for (const auto& pair : ageCount) {
        std::cout << "Age " << pair.first << ": " << pair.second << " occurrences\n";
    }

    return 0;
}
{% endraw %}
```

In this code, we initialize the 2D vector `myVector` with some sample data containing multiple rows of `Person` objects. Then, we define a `std::map` named `ageCount` to store the counts for each age.

We use nested for loops to iterate over each `Person` object in `myVector` and update the corresponding age count in `ageCount`. The expression `ageCount[person.age]++` retrieves the count associated with the current age and increments it.

Finally, we display the age counts by iterating over the `ageCount` map and printing each age and its occurrence count.

By using this approach, you can easily count the occurrences of a specific attribute within a 2D vector of custom objects, enabling you to perform further analysis or operations on the data based on these counts.

#cpp #codingtips