---
layout: post
title: "Design patterns that involve the use of functors in C++"
description: " "
date: 2023-09-14
tags: [include, DesignPatterns]
comments: true
share: true
---

C++ is a powerful and versatile programming language that provides various features for designing efficient and flexible software applications. Functors, also known as function objects, are a key concept in C++ that allow us to treat functions as objects. Functors can be used to encapsulate behavior and pass them as arguments to other functions, making them an integral part of many design patterns.

In this blog post, we will explore two design patterns that make use of functors in C++: the Strategy pattern and the Command pattern.

## Strategy Pattern

The Strategy pattern is a behavioral design pattern that enables us to define a family of algorithms, encapsulate each one as a class, and make them interchangeable at runtime. Functors are ideal for implementing the Strategy pattern as they can represent different algorithms through different operator overloads or function call operators.

Here's a simple example of implementing the Strategy pattern using functors in C++:

```cpp
#include <iostream>

class SortStrategy {
public:
    virtual void sort(int arr[], int size) = 0;
};

class BubbleSort : public SortStrategy {
public:
    void sort(int arr[], int size) override {
        // Implement bubble sort logic
    }
};

class QuickSort : public SortStrategy {
public:
    void sort(int arr[], int size) override {
        // Implement quick sort logic
    }
};

class Sorter {
private:
    SortStrategy* strategy;
public:
    void setSortStrategy(SortStrategy* strategy) {
        this->strategy = strategy;
    }
    
    void sort(int arr[], int size) {
        strategy->sort(arr, size);
    }
};

int main() {
    int arr[] = {5, 2, 8, 6, 1};
    int size = sizeof(arr) / sizeof(arr[0]);
    
    Sorter sorter;
    BubbleSort bubbleSort;
    QuickSort quickSort;
    
    sorter.setSortStrategy(&bubbleSort);
    sorter.sort(arr, size);
    
    // Output the sorted array
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    
    return 0;
}
```

In this example, the `SortStrategy` is an abstract base class that defines an interface for sorting algorithms. The `BubbleSort` and `QuickSort` classes implement the `SortStrategy` interface using different sorting algorithms. The `Sorter` class encapsulates the strategy and provides a method to set the sorting strategy at runtime.

## Command Pattern

The Command pattern is another behavioral design pattern that encapsulates a request as an object, thereby allowing clients to parameterize clients with queues, requests, and operations. Functors can be used to represent commands and provide the necessary logic to execute them.

Here's a simple example of the Command pattern using functors in C++:

```cpp
#include <iostream>
#include <vector>

class Command {
public:
    virtual void execute() = 0;
};

class PrintCommand : public Command {
private:
    std::string message;
public:
    PrintCommand(const std::string& message) : message(message) {}
    
    void execute() override {
        std::cout << message << std::endl;
    }
};

class CommandInvoker {
private:
    std::vector<Command*> commands;
public:
    void addCommand(Command* command) {
        commands.push_back(command);
    }
    
    void executeCommands() {
        for (Command* command : commands) {
            command->execute();
        }
    }
};

int main() {
    CommandInvoker invoker;
    PrintCommand printCommand1("Hello");
    PrintCommand printCommand2("World");
    
    invoker.addCommand(&printCommand1);
    invoker.addCommand(&printCommand2);
    
    invoker.executeCommands();
    
    return 0;
}
```

In this example, the `Command` class is an abstract base class that defines a uniform interface for commands. The `PrintCommand` class implements the `Command` interface and encapsulates a specific print command with a message. The `CommandInvoker` class maintains a collection of commands and provides a method to execute them.

By using functors as commands, the Command pattern becomes more dynamic and flexible, allowing clients to specify different behaviors at runtime.

## Conclusion

Functors provide a powerful mechanism for encapsulating functions as objects in C++. Design patterns such as the Strategy pattern and the Command pattern can leverage functors to create flexible and reusable code. Understanding and utilizing these design patterns can lead to cleaner code and more maintainable software applications.
 
`#C++ #DesignPatterns`