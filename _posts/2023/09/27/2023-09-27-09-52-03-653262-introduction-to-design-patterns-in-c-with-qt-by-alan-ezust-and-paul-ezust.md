---
layout: post
title: ""Introduction to Design Patterns in C++ with Qt" by Alan Ezust and Paul Ezust"
description: " "
date: 2023-09-27
tags: [designpatterns, cplusplus]
comments: true
share: true
---

Design patterns are reusable solutions to common problems that occur in software design. They provide a way to structure and organize code, making it easier to maintain and modify. In this blog post, we will introduce you to some popular design patterns in C++ using the Qt framework.

## Why use Design Patterns?

Design patterns can help improve the overall design of your software by promoting modular, flexible, and maintainable code. They provide a common vocabulary for communicating and sharing knowledge among developers. By following established patterns, you can reduce the time and effort required to develop robust software solutions.

## Creational Design Patterns

### Singleton Pattern

The Singleton pattern ensures that only one instance of a class is created and provides a global point of access to it. This can be useful when you need to limit the number of instances, such as in a database connection or logger class.

```cpp
class Logger {
private:
    static Logger* instance;
    Logger() {}

public:
    static Logger* getInstance() {
        if (instance == nullptr) {
            instance = new Logger();
        }

        return instance;
    }

    void log(const QString& message) {
        // Log the message
    }
};

Logger* Logger::instance = nullptr;
```

### Factory Pattern

The Factory pattern provides an interface for creating objects, but allows subclasses to decide which class to instantiate. This can be useful when you want to decouple the object creation logic from the calling code.

```cpp
class Shape {
public:
    virtual void draw() = 0;
};

class Circle : public Shape {
public:
    void draw() override {
        // Draw a circle
    }
};

class Square : public Shape {
public:
    void draw() override {
        // Draw a square
    }
};

class ShapeFactory {
public:
    static std::unique_ptr<Shape> createShape(const QString& type) {
        if (type == "circle") {
            return std::make_unique<Circle>();
        } else if (type == "square") {
            return std::make_unique<Square>();
        }

        return nullptr;
    }
};
```

## Structural Design Patterns

### Adapter Pattern

The Adapter pattern allows incompatible interfaces to work together. It acts as a bridge between two interfaces, converting the interface of one class into another that the client expects.

```cpp
class LegacyRectangle {
public:
    void drawRectangle(int x, int y, int width, int height) {
        // Draw a rectangle using legacy code
    }
};

class RectangleAdapter : public Shape {
private:
    LegacyRectangle legacyRectangle;

public:
    void draw() override {
        legacyRectangle.drawRectangle(0, 0, 100, 200);
        // Convert the legacy rectangle method call to the Shape interface
    }
};
```

## Behavioral Design Patterns

### Observer Pattern

The Observer pattern defines a one-to-many dependency between objects, where a change in one object triggers updates to all its dependents. It promotes loose coupling and allows objects to be easily notified of changes.

```cpp
class Subject {
private:
    QList<Observer*> observers;

public:
    void attachObserver(Observer* observer) {
        observers.append(observer);
    }

    void detachObserver(Observer* observer) {
        observers.removeOne(observer);
    }

    void notifyObservers() {
        for (auto observer : observers) {
            observer->update();
        }
    }
};

class Observer {
public:
    virtual void update() = 0;
};

class ConcreteObserver : public Observer {
    void update() override {
        // React to the subject's change
    }
};
```

## Conclusion

Design patterns are an essential part of software development, helping to improve code structure, modularity, and maintainability. In this blog post, we introduced you to some popular design patterns using C++ and the Qt framework. By leveraging these patterns, you can enhance your software design and create more robust and scalable applications.

#designpatterns #cplusplus #qt