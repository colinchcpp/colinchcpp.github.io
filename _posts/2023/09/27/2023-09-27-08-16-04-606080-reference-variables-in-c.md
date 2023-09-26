---
layout: post
title: "Reference variables in C++"
description: " "
date: 2023-09-27
tags: [References]
comments: true
share: true
---

To define a reference variable in C++, you use the `&` symbol after the variable type. Here's an example:

```cpp
#include <iostream>

int main() {
    int num = 10;
    int& ref = num; // reference variable to alias 'num'

    std::cout << "Value of num: " << num << std::endl;
    std::cout << "Value of ref: " << ref << std::endl;

    ref = 20; // modifying the value through the reference

    std::cout << "Value of num after modification: " << num << std::endl;

    return 0;
}
```

In this example, we define an integer variable `num` and a reference variable `ref` which is assigned the value of `num`. Any modifications made to `ref` will also modify `num` because `ref` is just an alias for `num`.

When executed, the output will be:

```
Value of num: 10
Value of ref: 10
Value of num after modification: 20
```

You can see that modifying `ref` also changes the value of `num`.

It's important to note that reference variables must be initialized when they are declared. Once a reference is assigned, it cannot be changed to refer to another variable. This makes it different from a traditional pointer.

References provide a convenient way to work with variables in C++. By using references, you can create a more readable and efficient code, especially when dealing with large data structures or passing variables between functions. 

#C++ #References