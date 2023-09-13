---
layout: post
title: "Design patterns and C++ OOP"
description: " "
date: 2023-09-13
tags: [include, designpatterns]
comments: true
share: true
---

Design patterns are proven solutions to recurring software design problems. They provide a structured approach to solving common programming challenges and promote code reusability, maintainability, and extensibility. In this blog post, we will explore some popular design patterns and how they can be implemented using **C++**.

## 1. Singleton Pattern

The **Singleton pattern** ensures that a class has only one instance globally accessible throughout the application. It is commonly used in scenarios where a single object needs to coordinate actions across different parts of the system.

```cpp
// C++ Singleton implementation

class Singleton {
private:
    static Singleton* instance;
    
    // Private constructor to prevent instantiation
    Singleton() {}

public:
    static Singleton* getInstance() {
        if (instance == nullptr) {
            instance = new Singleton();
        }
        return instance;
    }
};

Singleton* Singleton::instance = nullptr;
```
[Singleton Pattern](https://en.wikipedia.org/wiki/Singleton_pattern)

## 2. Observer Pattern

The **Observer pattern** establishes a one-to-many dependency between objects. When the state of one object changes, its dependent objects are notified and updated automatically. This pattern is useful in scenarios where there is a need for loose coupling between objects.

```cpp
// C++ Observer implementation

#include <vector>


class Observer {
public:
    virtual void update() = 0;
};


class Subject {
private:
    std::vector<Observer*> observers;

public:
    void attach(Observer* observer) {
        observers.push_back(observer);
    }

    void detach(Observer* observer) {
        // Detach observer from vector
    }

    void notify() {
        for (Observer* observer : observers) {
            observer->update();
        }
    }
};
```
[Observer Pattern](https://en.wikipedia.org/wiki/Observer_pattern)

These are just two examples of design patterns that can be implemented using **C++**. There are many other design patterns like Factory, Strategy, Decorator, and more, that can be applied to solve specific problems.

**#designpatterns #c++**