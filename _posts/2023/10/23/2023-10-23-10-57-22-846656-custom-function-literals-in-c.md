---
layout: post
title: "Custom function literals in C++"
description: " "
date: 2023-10-23
tags: [cplusplus, functionliterals]
comments: true
share: true
---

In C++, a function literal (also known as a lambda function or an anonymous function) is a convenient way to define a small, self-contained function without the need for a separate function declaration. It allows you to create functions on-the-fly, making your code more concise and expressive.

## Syntax

The syntax for defining a function literal in C++ is as follows:

```cpp
[Capture](Parameters) -> ReturnType {
    // Body of the function
}
```

Let's break down each component:

- `[Capture]`: This optional part is used to capture variables from the surrounding scope. It allows the function literal to access variables that are not passed as parameters.
- `(Parameters)`: The parameters of the function. These can be empty if the function doesn't require any parameters.
- `-> ReturnType`: The return type of the function. If the function doesn't return anything (void), you can omit this part.
- `{}`: The body of the function. This is where you define the logic of the function.

## Examples

Let's look at some examples to better understand how function literals work:

### Example 1: Basic Addition

```cpp
auto add = [](int a, int b) -> int {
    return a + b;
};

int result = add(3, 5);  // result = 8
```

In this example, we define a function literal named `add`. It takes two integers as parameters and returns their sum. We then call this function by passing `3` and `5`, and store the result in the variable `result`.

### Example 2: Capture Variables

```cpp
int multiplier = 2;
auto multiply = [multiplier](int num) -> int {
    return num * multiplier;
};

int result = multiply(5);  // result = 10
```

In this example, we define a function literal named `multiply`. It takes an integer as a parameter and multiplies it by the captured `multiplier` variable. We then call this function with `5`, and store the result in the variable `result`.

## Benefits of Function Literals

Using function literals in C++ offers several benefits:

1. **Conciseness**: Function literals allow you to define small, self-contained functions directly in your code, making it more concise and readable.
2. **Flexibility**: Function literals can be passed as arguments to other functions or stored in variables, giving you more flexibility in designing your code.
3. **Avoiding unnecessary function declarations**: With function literals, you can avoid the need for separate function declarations, reducing the clutter in your code.

## Conclusion

Custom function literals in C++ provide a powerful way to create small, anonymous functions on-the-fly. They allow you to write concise, expressive code by defining functions directly in your code without the need for separate function declarations. By using function literals, you can improve the readability and flexibility of your C++ programs. Give them a try in your next project! #cplusplus #functionliterals