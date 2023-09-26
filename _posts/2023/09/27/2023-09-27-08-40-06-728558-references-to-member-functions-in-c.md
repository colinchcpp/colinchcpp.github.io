---
layout: post
title: "References to member functions in C++"
description: " "
date: 2023-09-27
tags: [memberfunctions]
comments: true
share: true
---

## 1. Using the Member Function Pointer

One way to reference a member function in C++ is by using a member function pointer. A member function pointer is a pointer that points to a member function of a class. Here's an example of how to use a member function pointer:

```cpp
class MyClass {
public:
    void myMemberFunction() {
        std::cout << "Hello from MyClass!" << std::endl;
    }
};

int main() {
    typedef void (MyClass::*memberFunctionPtr)();
    memberFunctionPtr funcPtr = &MyClass::myMemberFunction;

    MyClass obj;
    (obj.*funcPtr)();  // Calling the member function using the pointer

    return 0;
}
```

In this example, we define a class `MyClass` with a member function `myMemberFunction()`. We then declare a member function pointer `funcPtr` of type `memberFunctionPtr`, which points to `myMemberFunction()`.

Inside the `main()` function, we create an instance of `MyClass` called `obj`. We then use the member function pointer to call `myMemberFunction()` on the object `obj`. The syntax `(obj.*funcPtr)()` is used to invoke the member function using the pointer.

## 2. Using the std::function Wrapper

Another way to reference member functions is by using the `std::function` wrapper from the C++ Standard Library. The `std::function` template provides a type-erasure mechanism that allows treating function pointers, member function pointers, and function objects as a single unified type. Here's an example:

```cpp
#include <functional>
#include <iostream>

class MyClass {
public:
    void myMemberFunction() {
        std::cout << "Hello from MyClass!" << std::endl;
    }
};

int main() {
    MyClass obj;
    std::function<void()> funcPtr = std::bind(&MyClass::myMemberFunction, &obj);

    funcPtr();  // Calling the member function using the function object

    return 0;
}
```

In this example, we include the `<functional>` header to use the `std::function` wrapper. Inside the `main()` function, we create an instance of `MyClass` called `obj`.

We then define a `std::function` object `funcPtr` that encapsulates the member function `myMemberFunction()` using the `std::bind` function. The `std::bind` function takes the member function's pointer as the first argument and the object instance pointer as the second argument.

Finally, we invoke the member function using the `funcPtr()` syntax.

## Conclusion

Referencing member functions in C++ can be done using member function pointers or the `std::function` wrapper. Both methods provide flexibility and allow you to access and call member functions within your code effectively. Understanding how to reference member functions is key to leveraging the full power and potential of object-oriented programming in C++.

#C++ #memberfunctions