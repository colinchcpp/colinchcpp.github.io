---
layout: post
title: "Overloading stream insertion and extraction operators in C++"
description: " "
date: 2023-09-14
tags: [OperatorOverloading]
comments: true
share: true
---

In C++, stream insertion (`<<`) and extraction (`>>`) operators are used to perform input and output operations on streams. By default, these operators are defined for built-in types and standard library classes. However, they can also be overloaded to work with user-defined types.

## Overloading the Stream Insertion Operator (<<)

The stream insertion operator (`<<`) is used to output data to a stream, such as `std::cout` or a `std::ofstream` object. To overload the `<<` operator for a user-defined class, we need to define a friend function or a member function with the following signature:

```cpp
std::ostream& operator<<(std::ostream& os, const MyClass& obj);
```

Here, `os` is a reference to the output stream, and `const MyClass& obj` is a reference to the object we want to output. The function should return the output stream `os` by reference to allow chaining multiple insertions.

For example, let's say we have a `Person` class with name and age attributes:

```cpp
class Person {
private:
    std::string name;
    int age;

public:
    // Constructor and other member functions...

    // Overload the << operator
    friend std::ostream& operator<<(std::ostream& os, const Person& p);
};

std::ostream& operator<<(std::ostream& os, const Person& p) {
    os << "Name: " << p.name << ", Age: " << p.age;
    return os;
}
```

Now, we can use the overloaded `<<` operator to output objects of the `Person` class:

```cpp
Person person("John", 25);
std::cout << person; // Output: Name: John, Age: 25
```

## Overloading the Stream Extraction Operator (>>)

The stream extraction operator (`>>`) is used to input data from a stream, such as `std::cin` or a `std::ifstream` object. To overload the `>>` operator for a user-defined class, we need to define a friend function or a member function with the following signature:

```cpp
std::istream& operator>>(std::istream& is, MyClass& obj);
```

Here, `is` is a reference to the input stream, and `MyClass& obj` is a reference to the object where we want to store the input. The function should return the input stream `is` by reference to allow chaining multiple extractions.

For example, let's say we have a `Book` class with title and author attributes:

```cpp
class Book {
private:
    std::string title;
    std::string author;

public:
    // Constructor and other member functions...

    // Overload the >> operator
    friend std::istream& operator>>(std::istream& is, Book& book);
};

std::istream& operator>>(std::istream& is, Book& book) {
    std::cout << "Enter book title: ";
    is >> book.title;
    
    std::cout << "Enter book author: ";
    is >> book.author;
    
    return is;
}
```

Now, we can use the overloaded `>>` operator to input objects of the `Book` class:

```cpp
Book book;
std::cin >> book; // Input: Enter book title: C++ in Action, Enter book author: Jane Smith
```

By overloading the stream insertion and extraction operators, we can customize the input and output behavior for user-defined classes. This allows us to seamlessly integrate our classes with the standard library's input and output mechanisms.

#C++ #OperatorOverloading