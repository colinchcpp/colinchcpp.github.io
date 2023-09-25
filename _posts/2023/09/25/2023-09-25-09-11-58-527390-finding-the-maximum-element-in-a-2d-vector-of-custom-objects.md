---
layout: post
title: "Finding the maximum element in a 2D vector of custom objects"
description: " "
date: 2023-09-25
tags: [programming]
comments: true
share: true
---

In many programming scenarios, we often encounter situations where we need to find the maximum element in a 2D vector of custom objects. This process involves iterating through the vector and comparing values based on a specific attribute or property of the custom objects.

In this blog post, we will explore how to tackle this problem using *C++* as our programming language of choice.

## Sample Custom Object

Before we dive into the solution, let's define a sample custom object for illustration purposes. Let's consider a class called `Person`, which has two attributes: `name` (string) and `age` (integer). Each object of this class represents a person with their name and age.

```cpp
class Person
{
public:
    std::string name;
    int age;
};
```

## Finding the Maximum Element

To find the maximum element in a 2D vector of `Person` objects, we will follow these steps:

1. Initialize a reference variable (`maxPerson`) to store the current maximum element. We will start with the first element of the 2D vector.
2. Iterate through each row (`subVector`) in the 2D vector.
3. Within each row, iterate through each column (`person`) containing `Person` objects.
4. Compare the age of the current `Person` object with the age of the `maxPerson` object. If the age is greater, update the `maxPerson` reference.
5. After iterating through all the elements, the `maxPerson` reference will contain the maximum element.

Here's an example implementation:

```cpp
Person findMaxPerson(const std::vector<std::vector<Person>>& people)
{
    // Step 1
    Person maxPerson = people[0][0];

    // Step 2
    for (const auto& subVector : people)
    {
        // Step 3
        for (const auto& person : subVector)
        {
            // Step 4
            if (person.age > maxPerson.age)
            {
                maxPerson = person;
            }
        }
    }

    // Step 5
    return maxPerson;
}
```

## Example Usage

Let's say we have a 2D vector called `allPeople` with multiple `Person` objects, and we want to find the person with the maximum age. We would use the `findMaxPerson` function like this:

```cpp
std::vector<std::vector<Person>> allPeople = {
    { {"John", 25}, {"Sarah", 30} },
    { {"Mark", 28}, {"Alice", 35} },
    { {"Emily", 22}, {"Michael", 24} }
};

Person maxAgePerson = findMaxPerson(allPeople);

std::cout << "Maximum Age Person: " << maxAgePerson.name << " (Age: " << maxAgePerson.age << ")" << std::endl;
```

In this example, the output would be:

```
Maximum Age Person: Alice (Age: 35)
```

## Conclusion

Finding the maximum element in a 2D vector of custom objects can be achieved by iterating through the elements and comparing specific attributes or properties. By following the steps outlined in this blog post, we were able to implement a solution using *C++*.

By applying these concepts, you can extend this approach to handle more complex scenarios or customize it to suit your specific needs.

#programming #C++