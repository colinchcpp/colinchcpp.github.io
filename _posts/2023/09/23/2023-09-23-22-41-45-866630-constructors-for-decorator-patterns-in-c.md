---
layout: post
title: "Constructors for Decorator Patterns in C++"
description: " "
date: 2023-09-23
tags: [DesignPatterns]
comments: true
share: true
---

When implementing the Decorator pattern in C++, constructors play a crucial role in composing the decorators and the core component. Constructors allow you to initialize the decorators and pass the core component as an argument.

In the Decorator pattern, decorators are classes that wrap the core component and provide additional functionality without altering its interface. This allows for dynamic behavior modification at runtime.

To illustrate the use of constructors in Decorator patterns, let's consider an example where we have a `Pizza` class as our core component, and we want to add decorators to modify its behavior.

## The Core Component

```cpp
class Pizza {
public:
    virtual void printDescription() const {
        std::cout << "Basic pizza" << std::endl;
    }
};
```

## Decorator Base Class

We start by defining a base class for the decorators. This class should inherit from the `Pizza` class to ensure that it can be used interchangeably with the core component.

```cpp
class PizzaDecorator : public Pizza {
protected:
    Pizza* pizza;

public:
    PizzaDecorator(Pizza* pizza) : pizza(pizza) {}
};
```

## Decorators

We can then create concrete decorators by deriving from the `PizzaDecorator` base class. Let's start with a `CheeseDecorator` that adds cheese topping to our pizza.

```cpp
class CheeseDecorator : public PizzaDecorator {
public:
    CheeseDecorator(Pizza* pizza) : PizzaDecorator(pizza) {}

    virtual void printDescription() const override {
        pizza->printDescription();
        std::cout << " + Cheese" << std::endl;
    }
};
```

Next, let's create a `VegetableDecorator` that adds vegetables as toppings to our pizza.

```cpp
class VegetableDecorator : public PizzaDecorator {
public:
    VegetableDecorator(Pizza* pizza) : PizzaDecorator(pizza) {}

    virtual void printDescription() const override {
        pizza->printDescription();
        std::cout << " + Vegetables" << std::endl;
    }
};
```

## Usage

We can now create instances of our core component `Pizza` and decorate them with additional functionality using the created decorators.

```cpp
int main() {
    Pizza* basicPizza = new Pizza();
    basicPizza->printDescription();
    // Output: Basic pizza

    Pizza* cheesePizza = new CheeseDecorator(basicPizza);
    cheesePizza->printDescription();
    // Output: Basic pizza + Cheese

    Pizza* veggiePizza = new VegetableDecorator(cheesePizza);
    veggiePizza->printDescription();
    // Output: Basic pizza + Cheese + Vegetables

    delete basicPizza;
    delete cheesePizza;
    delete veggiePizza;

    return 0;
}
```

By using constructors, we can easily create decorators that wrap around the core component and add additional functionality as desired.

#C++ #DesignPatterns