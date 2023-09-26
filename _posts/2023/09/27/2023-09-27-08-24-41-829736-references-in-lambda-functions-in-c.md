---
layout: post
title: "References in lambda functions in C++"
description: " "
date: 2023-09-27
tags: [LambdaFunctions, References]
comments: true
share: true
---

One commonly encountered scenario is passing references to variables within a lambda function. This can be achieved by specifying the capture list in the lambda expression. The capture list defines what variables from the surrounding scope should be accessible inside the lambda function.

Let's look at an example where we pass a reference to a variable inside a lambda function:

```cpp
#include <iostream>

int main() {
    int num = 5; // variable to be captured

    auto lambda = [&num]() {
        num += 10; // accessing and modifying the captured variable
        std::cout << "Inside lambda, num = " << num << std::endl;
    };

    lambda(); // calling the lambda function

    std::cout << "After lambda, num = " << num << std::endl;

    return 0;
}
```

In this code snippet, we have a variable `num` initialized to 5. We define a lambda function `lambda` that captures `num` by reference (`&num`). Inside the lambda function, we can access and modify the value of `num` directly.

On calling `lambda()`, the lambda function is executed, incrementing the value of `num` by 10 and printing it inside the lambda. The output will be:

```
Inside lambda, num = 15
After lambda, num = 15
```

As you can see, the lambda function is able to modify the captured reference `num` directly, with the changes reflected outside the function as well.

References in lambda functions provide a convenient way to work with variables from the surrounding scope, allowing for flexible and powerful code organization and functionality.

#C++ #LambdaFunctions #References