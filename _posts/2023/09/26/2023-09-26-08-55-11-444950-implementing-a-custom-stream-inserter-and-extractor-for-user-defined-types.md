---
layout: post
title: "Implementing a custom stream inserter and extractor for user-defined types"
description: " "
date: 2023-09-26
tags: [CustomStreamOperators]
comments: true
share: true
---

One of the powerful features of C++ is the ability to overload the stream insertion (`<<`) and extraction (`>>`) operators for custom user-defined types. This allows us to seamlessly stream objects of our own classes into and out of streams, such as `std::cout` and `std::cin`. In this blog post, we will walk through the process of implementing a custom stream inserter and extractor for a user-defined type.

### The Custom Type
Let's begin by defining a simple class called `Person` that represents a person's basic information, including their name and age.

```cpp
class Person {
private:
    std::string name;
    int age;
    
public:
    Person(const std::string& name, int age)
        : name(name), age(age) {}
        
    // ...
};
```

### Stream Insertion Operator
To enable streaming a `Person` object to an output stream, we need to overload the `<<` operator. This can be done as a friend function of the `Person` class:

```cpp
std::ostream& operator<<(std::ostream& os, const Person& person) {
    os << "Name: " << person.name << ", Age: " << person.age;
    return os;
}
```

Here, we simply output the respective member data of the `Person` object to the output stream.

### Stream Extraction Operator
To enable reading a `Person` object from an input stream, we need to overload the `>>` operator. Again, this can be done as a friend function of the `Person` class:

```cpp
std::istream& operator>>(std::istream& is, Person& person) {
    std::cout << "Enter name: ";
    std::getline(is, person.name);

    std::cout << "Enter age: ";
    is >> person.age;

    // Ignore remaining characters in the input stream
    is.ignore(std::numeric_limits<std::streamsize>::max(), '\n');

    return is;
}
```

In this implementation, we prompt the user to enter the name and age of the person. We use `std::getline` to read the name, as it allows us to handle inputs with spaces. Then we use `is >> person.age` to read the age. Finally, we ignore any remaining characters in the input stream to ensure it's in a clean state for the next input operation.

### Putting it all Together
Now, let's see our custom stream inserter and extractor in action:

```cpp
int main() {
    Person p1("John Doe", 28);

    std::cout << "Person p1: " << p1 << std::endl;

    Person p2;
    std::cout << "Enter person details: ";
    std::cin >> p2;

    std::cout << "Person p2: " << p2 << std::endl;
    
    return 0;
}
```

In this example, we create a `Person` object `p1` with a name and age and print it using the overloaded `<<` operator. Then, we create another `Person` object `p2` and take user input for its details using the overloaded `>>` operator, and finally display the entered details using the `<<` operator again.

### Conclusion
Implementing custom stream inserter and extractor operators allows us to seamlessly integrate our user-defined types with the C++ streams. It simplifies the process of input and output operations, making our code more concise and readable. By following the steps outlined in this blog post, you can easily implement custom stream insertion and extraction for your own user-defined types. #CPP #CustomStreamOperators