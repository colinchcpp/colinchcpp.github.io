---
layout: post
title: "Reference parameters in C++"
description: " "
date: 2023-09-27
tags: [ReferenceParameters]
comments: true
share: true
---

To define a reference parameter in C++, you can include an ampersand (&) symbol before the parameter name in the function signature. Here's an example:

```cpp
void swap(int& a, int& b) {
  int temp = a;
  a = b;
  b = temp;
}

int main() {
  int x = 5;
  int y = 10;

  std::cout << "Before swap: x = " << x << ", y = " << y << std::endl;

  swap(x, y);

  std::cout << "After swap: x = " << x << ", y = " << y << std::endl;

  return 0;
}
```

In the above example, the `swap` function takes two reference parameters `a` and `b`. Inside the function, the values of `a` and `b` are swapped using a temporary variable `temp`.

In the `main` function, two variables `x` and `y` are defined and assigned values. After calling the `swap` function, `x` and `y` are swapped because they were passed as reference parameters.

The output of the above code will be:

```
Before swap: x = 5, y = 10
After swap: x = 10, y = 5
```

Using reference parameters can be useful when you need to modify the value of a variable inside a function and have those changes reflected outside of the function. It provides a way to pass variables by reference rather than by value.

By using reference parameters effectively in your C++ code, you can write functions that can alter the state of variables directly, improving code readability and efficiency.

#C++ #ReferenceParameters