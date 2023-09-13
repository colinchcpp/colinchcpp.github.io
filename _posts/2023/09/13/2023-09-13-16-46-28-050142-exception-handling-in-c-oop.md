---
layout: post
title: "Exception handling in C++ OOP"
description: " "
date: 2023-09-13
tags: [ExceptionHandling]
comments: true
share: true
---

Exception handling is a crucial aspect of programming as it allows developers to gracefully handle unexpected runtime errors or exceptional conditions. In C++, exception handling is particularly useful in object-oriented programming (OOP) to ensure proper code flow and error recovery.

## Basics of Exception Handling in C++

C++ provides a built-in mechanism to handle exceptions using the `try`, `catch`, and `throw` keywords. Following is the basic syntax:

```cpp
try {
    // Code block where exceptions might occur
} 
catch (<exception_type> exception_var) {
    // Code block to handle the exception
}
```

- The `try` block encloses the code that may generate one or more exceptions.
- The `catch` block catches and handles the specified exception(s). You can have multiple `catch` blocks to handle different types of exceptions.

## Handling Exceptions in Object-Oriented Programming

In an object-oriented programming paradigm, exception handling can be applied at both the class and object levels. 

### Class-Level Exception Handling

#### Example

```cpp
class MyClass {
public:
    int divideNumbers(int a, int b) {
        if (b == 0) {
            throw DivideByZeroException();
        }
        return a / b;
    }
};

class DivideByZeroException {
public:
    void showErrorMsg() {
        std::cout << "Error: Division by zero is not allowed!" << std::endl;
    }
};

int main() {
    MyClass obj;
    try {
        int result = obj.divideNumbers(10, 0);
        std::cout << "Result: " << result << std::endl;
    } 
    catch(DivideByZeroException& ex) {
        ex.showErrorMsg();
    }
    return 0;
}
```
In the above example, the `MyClass` has a member function `divideNumbers` that performs division. If the divisor is zero, the member function throws a `DivideByZeroException`.

The `DivideByZeroException` is a custom exception class that contains an error message. In the `catch` block, we catch and handle the `DivideByZeroException`, calling the `showErrorMsg` function to display the error message.

### Object-Level Exception Handling

At times, it may be necessary to handle exceptions within objects, especially when dealing with complex systems or interactions between objects.

#### Example

```cpp
class BankAccount {
private:
    double balance;
public:
    void deposit(double amount) {
        // Deposit logic here
        if (amount <= 0) {
            throw InvalidAmountException();
        }
    }
};

class InvalidAmountException {
public:
    void handleException() {
        std::cout << "Error: Invalid deposit amount!" << std::endl;
    }
};

int main() {
    try {
        BankAccount account;
        account.deposit(-100); // Negative amount
    }
    catch (InvalidAmountException& ex) {
        ex.handleException();
    }
    return 0;
}
```

In the above example, the `BankAccount` class has a `deposit` function that checks if the amount to be deposited is valid (greater than zero). If the amount is invalid, it throws an `InvalidAmountException`.

The `InvalidAmountException` class is responsible for handling the exception by displaying an error message. In the `catch` block, we catch and handle the `InvalidAmountException`.

## Conclusion

Exception handling in C++ OOP allows developers to handle exceptional scenarios effectively. By using `try`, `catch`, and `throw`, you can handle exceptions both at the class and object levels, ensuring smooth error recovery and code flow. Remember to **always** handle exceptions gracefully to improve the robustness and reliability of your code.

\#C++ #ExceptionHandling