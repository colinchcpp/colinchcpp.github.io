---
layout: post
title: "Overloading logical operators in C++"
description: " "
date: 2023-09-14
tags: [programming, cplusplus]
comments: true
share: true
---

C++ allows you to **overload** operators, including logical operators such as `&&` (AND), `||` (OR), `!` (NOT), etc. Overloading logical operators allows you to define custom behavior when using these operators with objects of your own classes.

In this blog post, we will explore how to overload logical operators in C++ and demonstrate some examples for better understanding.

## Overloading && (AND) Operator

To overload the `&&` operator, we need to define a member function named `operator&&` inside our class. This function should take another object of the same class as an argument and return a `bool` value.

Here's an example of overloading the `&&` operator:

```cpp
class MyClass {
public:
    bool value;

    MyClass(bool val) : value(val) {}

    bool operator&&(const MyClass& obj) const {
        return value && obj.value;
    }
};
```

In the above code snippet, we define a class `MyClass` with a `bool` member variable `value`. We then overload the `&&` operator using the `operator&&` member function. This function checks the value of both objects and returns the result of the logical AND operation between them.

Now, let's see how we can use our overloaded `&&` operator:

```cpp
int main()
{
    MyClass obj1(true);
    MyClass obj2(false);

    if (obj1 && obj2) {
        std::cout << "Both objects evaluate to true.\n";
    } else {
        std::cout << "One or both objects evaluate to false.\n";
    }

    return 0;
}
```
Output:
```
One or both objects evaluate to false.
```

## Overloading || (OR) Operator

Similar to overloading `&&`, we can overload the `||` operator as well. Here's an example of overloading the `||` operator:

```cpp
class MyClass {
public:
    bool value;

    MyClass(bool val) : value(val) {}

    bool operator||(const MyClass& obj) const {
        return value || obj.value;
    }
};
```

In this example, we define a class `MyClass` with a `bool` member variable `value` and overload the `||` operator using the `operator||` member function. The function performs the logical OR operation between the values of both objects and returns the result.

Let's use our overloaded `||` operator:

```cpp
int main()
{
    MyClass obj1(true);
    MyClass obj2(false);

    if (obj1 || obj2) {
        std::cout << "At least one object evaluates to true.\n";
    } else {
        std::cout << "Both objects evaluate to false.\n";
    }

    return 0;
}
```

Output:
```
At least one object evaluates to true.
```

## Conclusion

Overloading logical operators in C++ allows you to define custom behavior for these operators when working with objects of your own classes. This gives you more flexibility and control over how these operators are used in your code. By following the examples in this blog post, you can start leveraging the power of operator overloading in your C++ programs.

#programming #cplusplus