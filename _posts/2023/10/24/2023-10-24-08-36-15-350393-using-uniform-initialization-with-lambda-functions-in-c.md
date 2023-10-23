---
layout: post
title: "Using uniform initialization with lambda functions in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In modern C++, lambda functions are a powerful feature that allows you to define anonymous functions inline. They are useful in scenarios where you need to pass a function as an argument or store it in a variable. 

One of the features introduced in C++11 is uniform initialization, which allows you to initialize variables using curly braces `{}`. This syntax can also be used with lambda functions, providing a concise and readable way to define them.

Here's an example of using uniform initialization with lambda functions in C++:

```cpp
#include <iostream>

int main() {
  // Define a lambda function using uniform initialization
  auto multiply = [](int x, int y) { return x * y; };

  // Call the lambda function
  int result = multiply(5, 7);

  std::cout << "Result: " << result << std::endl;

  return 0;
}
```

In the above code, we define a lambda function called `multiply` using the uniform initialization syntax. The lambda takes two integer parameters `x` and `y` and returns their product. 

To call the lambda function, we simply use the variable name followed by the arguments in parentheses, just like any other function. In this case, we pass `5` and `7` as arguments and assign the returned value to the variable `result`.

Running the program will output:

```
Result: 35
```

Using uniform initialization with lambda functions provides a clean and concise way to define and call them. It simplifies the syntax by eliminating the need for the `function` keyword and allows for inline function definitions.

With C++11 onwards, uniform initialization and lambda functions can be combined to write more expressive and readable code.  

---

**References:**
- [C++ Lambda Functions](https://en.cppreference.com/w/cpp/language/lambda)
- [Uniform Initialization in C++](https://en.cppreference.com/w/cpp/language/list_initialization)

**#cplusplus #lambdafunctions**