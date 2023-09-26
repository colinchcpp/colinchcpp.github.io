---
layout: post
title: "Reference member variables in C++"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

Let's consider an example where we have a class called "Person" with two member variables: "name" and "age".

```cpp
class Person {
public:
  std::string name;
  int age;
};

int main() {
  Person person1; // Create an instance of the Person class
  
  // Assign values to the member variables
  person1.name = "John Doe";
  person1.age = 30;
  
  // Access the member variables using the instance
  std::cout << "Name: " << person1.name << std::endl;
  std::cout << "Age: " << person1.age << std::endl;

  return 0;
}
```

In the code above, we create an instance of the `Person` class named `person1`. Then, we assign values to the `name` and `age` member variables using the dot operator (`.`). Finally, we access and print the values of the member variables using the instance `person1` and the dot operator.

It's important to note that member variables can also be accessed using pointers to objects. If you have a pointer to an object, you can use the arrow operator (`->`) to reference the member variables instead of the dot operator. Here's an example:

```cpp
Person* personPtr = new Person(); // Create a pointer to a Person object

// Assign values to the member variables using the pointer
personPtr->name = "Jane Smith";
personPtr->age = 25;

// Access the member variables using the pointer
std::cout << "Name: " << personPtr->name << std::endl;
std::cout << "Age: " << personPtr->age << std::endl;

delete personPtr; // Remember to delete the dynamically allocated object
```

In this example, we create a pointer to a `Person` object named `personPtr`. We can access and assign values to the member variables using the arrow operator (`->`). Finally, don't forget to free the memory allocated for the object using the `delete` keyword.

That's how you can reference member variables in C++. By using an instance of the class or a pointer to an object, you can access and manipulate the member variables to effectively work with the data associated with each object.