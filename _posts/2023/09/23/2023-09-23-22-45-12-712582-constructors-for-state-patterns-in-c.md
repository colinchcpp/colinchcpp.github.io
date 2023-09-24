---
layout: post
title: "Constructors for State Patterns in C++"
description: " "
date: 2023-09-23
tags: [StatePattern]
comments: true
share: true
---

The State pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes. It is widely used in software development to build flexible and maintainable code.

In C++, constructors are essential for initializing objects with a specific state. When implementing the State pattern, constructors play a crucial role in setting up the initial state of the context object and assigning the appropriate state object.

Let's consider an example scenario where we have a `Context` class that can be in different states, such as "Idle", "Working", and "Sleeping". We will create state classes `IdleState`, `WorkingState`, and `SleepingState`, each representing a specific state of the `Context`.

### Constructor Implementation

Here's an example implementation of the constructors for the state classes:

```cpp
class Context;

class State {
public:
    virtual void handle(Context& context) = 0;
};

class IdleState : public State {
public:
    IdleState() {
        // Constructor code specific to IdleState
    }

    virtual void handle(Context& context) override {
        // Handle method implementation for IdleState
    }
};

class WorkingState : public State {
public:
    WorkingState() {
        // Constructor code specific to WorkingState
    }

    virtual void handle(Context& context) override {
        // Handle method implementation for WorkingState
    }
};

class SleepingState : public State {
public:
    SleepingState() {
        // Constructor code specific to SleepingState
    }

    virtual void handle(Context& context) override {
        // Handle method implementation for SleepingState
    }
};
```

In the above code snippet, we have defined the state classes `IdleState`, `WorkingState`, and `SleepingState`, each inheriting from the `State` base class. The constructor for each state class can contain code specific to that state, allowing us to define the initial conditions.

### Usage Example

Here's an example usage of the state classes with the `Context` class:

```cpp
class Context {
private:
    State* currentState;
public:
    Context(State* initialState) {
        currentState = initialState;
    }

    void setState(State* newState) {
        currentState = newState;
    }

    void handleRequest() {
        currentState->handle(*this);
    }
};

int main() {
    Context context(new IdleState());

    context.handleRequest(); // Outputs: "Handling request in IdleState"

    context.setState(new WorkingState());
    context.handleRequest(); // Outputs: "Handling request in WorkingState"

    context.setState(new SleepingState());
    context.handleRequest(); // Outputs: "Handling request in SleepingState"

    return 0;
}
```

In this usage example, we create a `Context` object with an initial state of `IdleState`. We then demonstrate how to change the state using the `setState` method.

By implementing the State pattern and utilizing constructors for the state classes, we can easily manage and handle different states in our application.

Remember, constructors are crucial for setting up the initial state of objects when implementing the State pattern in C++. They allow us to encapsulate state-specific logic and ensure a well-defined starting point for the objects.

#StatePattern #C++