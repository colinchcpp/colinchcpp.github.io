---
layout: post
title: "Constructors for Observer Patterns in C++"
description: " "
date: 2023-09-23
tags: [programming, designpatterns]
comments: true
share: true
---

The Observer pattern is a behavioral design pattern that allows an object, known as the subject, to notify a list of observers whenever its state changes. One of the key components of implementing the Observer pattern in C++ is the constructors for both the subject and observer classes.

## Subject Class Constructor

The subject class is responsible for managing the list of observers and notifying them when its state changes. Here is an example of a subject class constructor:

```cpp
class Subject {
public:
    Subject() {
        observers = new std::vector<Observer*>();
    }

    ~Subject() {
        delete observers;
    }

    void attachObserver(Observer* observer) {
        observers->push_back(observer);
    }

    void detachObserver(Observer* observer) {
        observers->erase(std::remove(observers->begin(), observers->end(), observer), observers->end());
    }

    void notifyObservers() {
        for (Observer* observer : *observers) {
            observer->update();
        }
    }

private:
    std::vector<Observer*>* observers;
};
```

In the constructor, we initialize the list of observers as a dynamic vector. We also need to provide a destructor to free the memory allocated for the list.

## Observer Class Constructor

The observer class defines the behavior that needs to be executed when the state of the subject changes. Here is an example of an observer class constructor:

```cpp
class Observer {
public:
    Observer() {
        // Constructor implementation
    }

    virtual ~Observer() {
        // Destructor implementation
    }

    virtual void update() = 0;
};
```

In the constructor, you can add any initialization code specific to the observer class. It is important to note that the observer class should be defined as an abstract class (using a pure virtual function) since there is no default implementation for the `update()` function.

## Conclusion

Constructors play a crucial role in implementing the Observer pattern in C++. The subject class constructor is responsible for initializing the list of observers, while the observer class constructor is used for any specific initialization code. By properly implementing these constructors, you can create a flexible and robust Observer pattern in your C++ projects.

#programming #designpatterns