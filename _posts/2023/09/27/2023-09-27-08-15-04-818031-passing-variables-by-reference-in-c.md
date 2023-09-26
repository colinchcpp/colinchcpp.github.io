---
layout: post
title: "Passing variables by reference in C++"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

To pass a variable by reference in C++, we use the "&" symbol in the function declaration. Let's look at an example to understand how it works:

```cpp
#include <iostream>

void modifyValue(int& num) {
    num = 10; // Modify the original variable directly
}

int main() {
    int num = 5;
    std::cout << "Before modification: " << num << "\n";
    
    modifyValue(num); // Pass `num` by reference
    
    std::cout << "After modification: " << num << "\n";
    
    return 0;
}
```

In this example, we have a function `modifyValue`, which takes an integer variable `num` by reference. Inside the function, we directly change the value of `num` to 10. When we call `modifyValue` from the `main` function and pass `num` as an argument, the original `num` variable gets modified.

The output of this code will be:

```
Before modification: 5
After modification: 10
```

By passing variables by reference, we eliminate the need to return a modified value from a function. This can be especially useful when dealing with large objects or when we want to modify multiple variables within a single function.

Remember to use this feature judiciously, as it can introduce side effects and make the code harder to reason about.