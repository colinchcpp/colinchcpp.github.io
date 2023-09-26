---
layout: post
title: "References in qualified names in C++"
description: " "
date: 2023-09-27
tags: [QualifiedNames]
comments: true
share: true
---

To understand references in qualified names, let's consider the following example:

```cpp
#include <iostream>

namespace myNamespace {
    int value = 42;
}

int main() {
    int& ref = myNamespace::value;

    std::cout << "Value: " << ref << std::endl;

    return 0;
}
```

In this example, we have a variable named `value` declared within the namespace `myNamespace`. We then define a reference `ref` to this variable. The qualified name `myNamespace::value` allows us to access the variable within that namespace and create a reference to it.

When we assign `myNamespace::value` to `ref`, we are creating an alias for that variable. Any changes made to `ref` will also affect the original variable `value` within the `myNamespace` namespace. In this case, both `ref` and `myNamespace::value` refer to the same memory location.

Finally, we print the value of `ref` using `std::cout`. Since `ref` is an alias for `myNamespace::value`, the output will be `42`.

Using qualified names with references allows us to access variables within different namespaces or classes and create aliases that can be used interchangeably. It provides flexibility and clarity in cases where multiple variables have the same name across different scopes.

#C++ #QualifiedNames