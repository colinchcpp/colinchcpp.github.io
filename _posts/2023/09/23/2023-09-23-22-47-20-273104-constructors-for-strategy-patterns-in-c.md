---
layout: post
title: "Constructors for Strategy Patterns in C++"
description: " "
date: 2023-09-23
tags: [StrategyPattern]
comments: true
share: true
---

In C++, constructors are essential to initialize objects of a class. When implementing the Strategy pattern, constructors play a crucial role in creating and setting up the appropriate strategy object for the context.

Let's consider an example scenario where we have a PaymentStrategy class that represents a payment method, and it has two concrete strategies - CreditCard and PayPal. The constructors for these strategies can be implemented as follows:

```cpp
// PaymentStrategy.h
class PaymentStrategy {
public:
    virtual ~PaymentStrategy() {} // virtual destructor for polymorphism
    
    virtual void pay(double amount) const = 0; // abstract pay function
};

class CreditCard : public PaymentStrategy {
private:
    std::string cardNumber;
    std::string expiryDate;
    std::string cvv;

public:
    // Constructor for CreditCard strategy
    CreditCard(const std::string& cardNumber, const std::string& expiryDate, const std::string& cvv)
        : cardNumber(cardNumber), expiryDate(expiryDate), cvv(cvv) {}

    void pay(double amount) const override {
        // Logic for making payment using Credit Card
        std::cout << "Payment of $" << amount << " using Credit Card - " << cardNumber << std::endl;
    }
};

class PayPal : public PaymentStrategy {
private:
    std::string email;
    std::string password;

public:
    // Constructor for PayPal strategy
    PayPal(const std::string& email, const std::string& password)
        : email(email), password(password) {}

    void pay(double amount) const override {
        // Logic for making payment using PayPal
        std::cout << "Payment of $" << amount << " using PayPal - " << email << std::endl;
    }
};
```

In the above example, the constructors of the `CreditCard` and `PayPal` classes accept specific parameters required for each payment method. The constructor initializes the member variables of the respective class.

By having these constructors, we can create objects of `CreditCard` and `PayPal` strategies and pass them to the payment context accordingly.

Using the Strategy pattern with appropriate constructors in C++ allows us to easily switch between different payment strategies without modifying the existing codebase extensively. This enables us to add new payment strategies in the future with minimal effort.

#C++ #StrategyPattern