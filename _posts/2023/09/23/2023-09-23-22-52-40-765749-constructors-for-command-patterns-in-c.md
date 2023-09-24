---
layout: post
title: "Constructors for Command Patterns in C++"
description: " "
date: 2023-09-23
tags: [CommandPattern, Constructors]
comments: true
share: true
---

When implementing the Command design pattern in C++, constructors play an important role in initializing objects and establishing the necessary connections between the invoker and the receiver. In this blog post, we will explore different approaches to designing constructors for Command objects in C++.

## Basic Constructor

The most basic implementation of a Command constructor takes a pointer to a receiver object as a parameter. This allows the Command object to hold a reference to the receiver and invoke its methods when necessary. Here's an example:

```cpp
class Command {
public:
    Command(Receiver* receiver) {
        receiver_ = receiver;
    }

    virtual void execute() = 0;

protected:
    Receiver* receiver_;
};
```
  
## Parameterized Constructor

In some cases, you may want to pass additional parameters to the Command object at the time of its instantiation. This can be achieved by adding extra parameters to the constructor. Here's an example:

```cpp
class Command {
public:
    Command(Receiver* receiver, const std::string& arg) {
        receiver_ = receiver;
        arg_ = arg;
    }

    virtual void execute() = 0;

protected:
    Receiver* receiver_;
    std::string arg_;
};
```

## Configurable Constructor

To make the Command object more flexible and configurable, you can design a constructor that accepts a configuration object or a set of key-value pairs. This allows the invoker to dynamically configure the Command object before executing it. Here's an example:

```cpp
class Command {
public:
    Command(Receiver* receiver, const std::unordered_map<std::string, std::string>& config) {
        receiver_ = receiver;
        config_ = config;
    }

    virtual void execute() = 0;

protected:
    Receiver* receiver_;
    std::unordered_map<std::string, std::string> config_;
};
```

## Conclusion

Constructors play a crucial role in setting up Command objects in the Command design pattern. Depending on your requirements, you can use basic constructors, parameterized constructors, or configurable constructors to initialize the Command objects. By choosing the appropriate constructor, you can ensure that your Command objects are properly initialized and ready to execute their designated tasks.

#cpp #CommandPattern #Constructors