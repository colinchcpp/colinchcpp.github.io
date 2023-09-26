---
layout: post
title: "Implementing custom stream insertion and extraction operators for complex types"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

In C++, the `iostream` library provides the ability to perform input and output operations using streams. By default, the library provides stream insertion (`<<`) and extraction (`>>`) operators for basic data types such as integers and strings. However, it is also possible to define custom stream inserters and extractors for complex types in order to provide a more intuitive way of inputting and outputting data.

Let's assume we have a complex type called `Person` with two data members: `name` (string) and `age` (integer). We can implement custom stream insertion and extraction operators for this `Person` type to simplify the input and output operations.

```cpp
#include <iostream>
#include <string>

class Person {
private:
    std::string name;
    int age;

public:
    Person(const std::string& name, int age) : name(name), age(age) {}

    // Define custom stream insertion operator (<<)
    friend std::ostream& operator<<(std::ostream& out, const Person& person) {
        out << "Name: " << person.name << ", Age: " << person.age;
        return out;
    }

    // Define custom stream extraction operator (>>)
    friend std::istream& operator>>(std::istream& in, Person& person) {
        std::cout << "Enter name: ";
        std::getline(in, person.name);

        std::cout << "Enter age: ";
        in >> person.age;

        // Clear the input buffer
        in.ignore(std::numeric_limits<std::streamsize>::max(), '\n');

        return in;
    }
};

int main() {
    Person p;

    // Input
    std::cin >> p;

    // Output
    std::cout << p << std::endl;

    return 0;
}
```

In the above example, we have defined the `Person` class with its constructor. We then define the custom stream insertion operator (`operator<<`) as a friend function, which allows it to access the private members of the `Person` class. This operator is responsible for outputting the `Person` object's data to the output stream (`std::ostream`).

Similarly, we define the custom stream extraction operator (`operator>>`) as a friend function. This operator takes input from the input stream (`std::istream`) and assigns it to the `Person` object's data members. We use `std::getline` to read the name with spaces.

Finally, in the `main` function, we create a `Person` object, input its data using the custom stream extraction operator, and output the object's data using the custom stream insertion operator.

By implementing these custom stream insertion and extraction operators, we can now perform input and output operations on `Person` objects in a more concise and readable manner, making the code more intuitive and easier to understand.

#CustomStreamOperators #C++