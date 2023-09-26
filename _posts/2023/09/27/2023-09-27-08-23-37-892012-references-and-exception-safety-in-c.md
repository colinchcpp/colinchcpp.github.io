---
layout: post
title: "References and exception safety in C++"
description: " "
date: 2023-09-27
tags: [hashtags]
comments: true
share: true
---

In C++, a reference is an alias for an existing object. It allows us to create additional names or aliases for variables. Unlike pointers, references must be initialized at the time of declaration and cannot be changed later to point to another object.

Here's an example of how to declare and use references in C++:

```cpp
int main() {
  int num = 10;
  int& ref = num; // declaring a reference to num
  
  cout << "Value of num: " << num << endl; // prints 10
  cout << "Value of ref: " << ref << endl; // prints 10

  num = 20; // changing the value of num

  cout << "Updated value of num: " << num << endl; // prints 20
  cout << "Value of ref after update: " << ref << endl; // also prints 20

  return 0;
}
```

In the code above, we declare a reference `ref` to the `num` variable. Both `num` and `ref` refer to the same memory location. Any changes made to `num` will also be reflected in `ref`, and vice versa.

# Exception Safety in C++

Exception safety is a term used in C++ to describe how a program handles exceptions and ensures that no resources are leaked or left in an inconsistent state during exception handling. Exception safety can be classified into three levels:

1. **No-Throw Guarantee**: A function provides the strongest exception safety guarantee by ensuring that no exceptions will be thrown. This level of exception safety guarantees that the program will not enter an invalid state even in the presence of exceptions.

2. **Basic Guarantee**: A function provides a basic level of exception safety if it guarantees that all resources are properly released and no memory leaks occur, even in the case of an exception. However, the object or program state may be left in an inconsistent or unspecified state.

3. **Strong Guarantee**: A function provides a strong exception safety guarantee if it ensures that if an exception is thrown, the program state remains unchanged. If the operation fails or throws an exception, any changes made prior to the operation will be rolled back, leaving the program in a valid and consistent state.

Here's an example that demonstrates exception safety using the Standard Library's `std::string` class:

```cpp
void concatenate(std::string& dest, const std::string& src) {
  std::string temp = dest; // create a copy of dest

  try {
    temp += src; // concatenate src to temp
    dest = temp; // update dest with the concatenated string
  } catch (...) {
    // in case of exception, dest is not modified
  }
}
```

In the code above, we create a temporary copy of the `dest` string and attempt to concatenate the `src` string to it. If an exception is thrown during the concatenation, the `catch` block ensures that the `dest` string remains unchanged. This provides a strong guarantee that the program state will not be modified if an exception occurs during the operation.

By understanding and applying exception safety principles in C++, we can write more robust and reliable code that handles exceptions gracefully and maintains program integrity.

#hashtags #C++