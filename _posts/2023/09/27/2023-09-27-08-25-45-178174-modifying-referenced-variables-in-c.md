---
layout: post
title: "Modifying referenced variables in C++"
description: " "
date: 2023-09-27
tags: [References]
comments: true
share: true
---

In C++, you can use references to modify the original value of a variable. A reference is an alias for an existing variable, allowing you to access and modify its value directly. By passing a variable as a reference to a function, you can modify its value outside of that function. Let's take a look at an example:

```cpp
#include <iostream>

// Function that modifies the referenced variable
void modifyValue(int& num) {
    num = 10;
}

int main() {
    int num = 5;

    std::cout << "Before modification: " << num << std::endl;

    // Pass the variable as a reference to the function
    modifyValue(num);

    std::cout << "After modification: " << num << std::endl;

    return 0;
}
```

In the above example, we have a function `modifyValue` that takes an integer reference as a parameter. Inside the function, we modify the value of the referenced variable to 10. In the `main` function, we declare an integer `num` and display its initial value. We then call the `modifyValue` function and pass `num` as a reference. After the function call, we display the updated value of `num` and observe that it has been modified to 10.

Using references to modify variables is a powerful feature in C++. It allows for efficient and clean code, as you don't need to return values from functions or use pointers to achieve similar behavior. Remember that when passing a variable as a reference, any changes made to it inside the function will affect the original variable outside of the function.

#C++ #References