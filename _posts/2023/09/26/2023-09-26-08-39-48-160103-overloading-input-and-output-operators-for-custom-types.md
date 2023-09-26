---
layout: post
title: "Overloading input and output operators for custom types"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

In C++, input and output operations can be performed on standard data types such as `int`, `float`, and `string` using the `cin` and `cout` objects. However, for custom types that you create, these operations must be explicitly defined.

To enable input and output operations on custom types, you can overload the input and output operators (`>>` and `<<`) respectively. This allows you to define how your custom type should be read from and written to standard input and output streams.

Let's say we have a custom class called `Person` with two member variables - `name` of type `string` and `age` of type `int`. We can overload the input and output operators for this class to allow easy input and output of `Person` objects.

## Overloading the Input and Output Operators

To overload the `>>` and `<<` operators for the `Person` class, we define them as standalone functions that take a reference to a `istream` or `ostream` object as the left-hand operand and a reference to a `Person` object as the right-hand operand.

Here's an example of how these functions can be implemented:

```cpp
#include <iostream>
#include <string>

class Person {
public:
    std::string name;
    int age;

    friend std::istream& operator>>(std::istream& input, Person& person) {
        input >> person.name >> person.age;
        return input;
    }

    friend std::ostream& operator<<(std::ostream& output, const Person& person) {
        output << "Name: " << person.name << ", Age: " << person.age;
        return output;
    }
};
```

In the example above, we define the `>>` operator as a friend function, which allows it to access the private member variables of the `Person` class. The `>>` operator reads the `name` and `age` from the input stream and assigns them to the corresponding member variables of the `person` object.

Similarly, we define the `<<` operator as a friend function to enable access to the private member variables. It writes the `name` and `age` of the `person` object to the output stream.

## Using the Overloaded Operators

Once we've overloaded the input and output operators for the `Person` class, we can easily use them for input and output operations. Here's an example of how to use these operators:

```cpp
int main() {
    Person person1;
    std::cout << "Enter name and age: ";
    std::cin >> person1;

    std::cout << "Person Details: " << person1 << std::endl;

    return 0;
}
```

In the code above, we create a `Person` object `person1`. We then use the overloaded `>>` operator to read the `name` and `age` of the person from the input stream. Finally, we use the overloaded `<<` operator to display the person's details on the output stream.

## Conclusion

Overloading the input and output operators (`>>` and `<<`) for custom types allows you to define how those types should be read from and written to standard input and output streams. This can greatly simplify the process of inputting and outputting objects of custom classes in C++, making your code more concise and readable.

#cpp #operators