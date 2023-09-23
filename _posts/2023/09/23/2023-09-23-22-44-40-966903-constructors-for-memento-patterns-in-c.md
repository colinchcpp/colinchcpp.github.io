---
layout: post
title: "Constructors for Memento Patterns in C++"
description: " "
date: 2023-09-23
tags: [memento, CPlusPlus]
comments: true
share: true
---

The Memento design pattern is a behavioral pattern that allows us to capture and store the internal state of an object without violating encapsulation. This pattern is useful when we need to undo or roll back changes in an object's state.

In C++, the Memento pattern typically involves three classes: the `Originator`, `Memento`, and `Caretaker`. The `Originator` class represents the object whose state we want to capture. The `Memento` class is responsible for storing the state of the `Originator`. The `Caretaker` class manages and retrieves the `Mementos` created by the `Originator`.

To implement the Memento pattern in C++, constructors play an important role. Here is an example of how constructors can be used in each of the relevant classes:

## Originator Class

The `Originator` class represents the object whose state needs to be captured. It is responsible for creating `Mementos` and restoring its state from `Mementos`. Here is an example of a basic `Originator` class with a constructor:

```cpp
class Originator {
private:
    std::string state;

public:
    Originator(const std::string& initState) : state(initState) {}

    std::string GetState() const {
        return state;
    }

    Memento CreateMemento() {
        return Memento(state);
    }

    void RestoreMemento(const Memento& memento) {
        state = memento.GetSavedState();
    }
};
```

In this example, the `Originator` class has a constructor that takes an initial state parameter and sets the `state` member variable accordingly. The `CreateMemento` function creates a `Memento` object with the current state of the `Originator`, which can be saved by the `Caretaker` for future restoration. The `RestoreMemento` function restores the state of the `Originator` from a given `Memento` object.

## Memento Class

The `Memento` class is responsible for storing the state of the `Originator`. It should provide methods to retrieve and set the saved state. Here is an example of a simple `Memento` class with a constructor:

```cpp
class Memento {
private:
    std::string savedState;

public:
    Memento(const std::string& state) : savedState(state) {}

    std::string GetSavedState() const {
        return savedState;
    }
};
```

The `Memento` class has a constructor that takes the current state of the `Originator` and saves it in the `savedState` member variable. The `GetSavedState` function allows external entities, such as the `Originator` or `Caretaker`, to retrieve the saved state.

## Caretaker Class

The `Caretaker` class manages multiple `Mementos` created by the `Originator`. It is responsible for saving and retrieving `Mementos` as needed. Here is an example of a basic `Caretaker` class with a constructor:

```cpp
class Caretaker {
private:
    std::vector<Memento> mementos;

public:
    void AddMemento(const Memento& memento) {
        mementos.push_back(memento);
    }

    Memento GetMemento(int index) const {
        return mementos[index];
    }
};
```

In this example, the `Caretaker` class has a constructor and two methods. The `AddMemento` function allows the `Originator` to add a `Memento` to the collection maintained by the `Caretaker`. The `GetMemento` function enables the `Originator` to retrieve a specific `Memento` from the collection.

## Conclusion

Constructors play a crucial role in implementing the Memento pattern in C++. They are responsible for initializing the state of the `Originator`, saving the state in `Mementos`, and providing methods for retrieving and setting the saved state.

By utilizing constructors effectively, we can successfully implement the Memento pattern to capture and restore the state of objects, thus enabling features like undo and rollback in our applications.

#memento #CPlusPlus