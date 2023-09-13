---
layout: post
title: "Friend classes and functions in C++"
description: " "
date: 2023-09-13
tags: [FriendClass, FriendFunction]
comments: true
share: true
---

In C++, you can define friend classes and functions to grant them access to private and protected members of a class. This feature is useful when you want to allow specific external functions or classes to manipulate the private members of a class without violating encapsulation. Let's explore how friend classes and functions work in C++.

## Friend Functions

A friend function is a standalone function that is not a member of a class but has access to its private and protected members. To declare a friend function, you need to declare it inside the class, preceded by the `friend` keyword.

```cpp
class MyClass {
private:
    int privateData;

    friend void friendFunction(); // Declare friend function

public:
   // ...
};

void friendFunction() {
   MyClass obj;
   obj.privateData = 42; // Access private member
}
```

In the above example, the `friendFunction` becomes a friend of the `MyClass`. So, it can access and modify the private member `privateData` of `MyClass`. Note that friend functions don't have any access specifiers.

## Friend Classes

Similar to friend functions, you can also declare an entire class as a friend of another class. By doing so, the friend class can access the private and protected members of the class it is declared as a friend.

```cpp
class MyClass {
private:
    int privateData;

    friend class FriendClass; // Declare FriendClass as friend

public:
    // ...
};

class FriendClass {
public:
    void accessPrivateData(MyClass& obj) {
        obj.privateData = 42; // Access private member
    }
};
```

In the above example, `FriendClass` is declared as a friend of `MyClass`. It can access and modify the private member `privateData` of `MyClass`.

## Usage and Considerations

The concept of friend classes and functions should be used with caution, as it can potentially break encapsulation and lead to code that is hard to maintain. However, there are certain scenarios where friend classes and functions can be beneficial, such as when implementing certain design patterns or when implementing overloaded operators.

It's important to note that the friendship is not reciprocal. Just because `ClassA` is a friend of `ClassB`, it doesn't imply that `ClassB` is a friend of `ClassA`. Additionally, friend functions and classes are not inherited, so the access granted by friendship does not extend to derived classes.

In conclusion, friend classes and functions in C++ provide a mechanism to grant specific external entities with access to the private and protected members of a class. While they can be handy in certain situations, it is important to use them judiciously and consider the potential impact on encapsulation and code maintainability.

**#C++ #FriendClass #FriendFunction**