---
layout: post
title: "Techniques for overloading function call operator in C++"
description: " "
date: 2023-09-14
tags: [FunctionOverloading]
comments: true
share: true
---

In C++, the function call operator `()` can be overloaded for a class to enable the object of that class to be callable like a function. This allows objects to be used as function-like entities, providing a convenient way to execute operations on the objects.

Here are some techniques for overloading the function call operator in C++:

## Technique 1: Function Call Operator Overloading

To overload the function call operator in C++, you need to define a member function named `operator()` inside a class. Here's an example:

```cpp
class Functor {
public:
    int operator()(int x, int y) {
        return x + y;
    }
};

int main() {
    Functor object;
    int result = object(3, 5); // Equivalent to calling object.operator()(3, 5)
    return 0;
}
```
In the above example, the `operator()` function is overloaded inside the `Functor` class, allowing objects of this class to be called as if they were functions. The `operator()` takes two `int` parameters and returns their sum. Inside the `main()` function, we create an object of the `Functor` class and use the function call operator `()` to invoke the overloaded operator, which adds 3 and 5 together.

## Technique 2: Lambda Functions

Lambda functions in C++ provide a concise way to define anonymous functions. They can be used to overload the function call operator as well. Here's an example:

```cpp
auto lambda = [](int x, int y) {
    return x + y;
};

int main() {
    int result = lambda(3, 5); // Equivalent to calling lambda.operator()(3, 5)
    return 0;
}
```

In this example, we define a lambda function `lambda` that takes two `int` parameters and returns their sum. We can directly invoke this lambda function using the function call operator `()`.

## Conclusion

Overloading the function call operator in C++ allows objects to be called as if they were functions. This provides flexibility and allows for more expressive code. These two techniques - function call operator overloading and lambda functions - are handy tools to achieve this functionality.

#C++ #FunctionOverloading