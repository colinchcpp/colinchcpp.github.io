---
layout: post
title: "Implementing type-safe function composition using variadic templates in C++"
description: " "
date: 2023-09-14
tags: [cplusplus, functioncomposition]
comments: true
share: true
---

Function composition is a powerful technique in functional programming that allows us to combine functions together to create new functions. In C++, we can implement type-safe function composition using variadic templates. This approach ensures that the types of the input and output of the composed functions match up correctly.

## What is Variadic Templates?

Variadic templates are a feature introduced in C++11 that allow us to define functions and classes that can take a variable number of arguments of arbitrary types. This feature enables us to work with a flexible number of inputs when implementing function composition.

## Implementing Function Composition

To implement type-safe function composition using variadic templates, we can define a template function called `compose` that takes multiple functions as arguments. Each function in the composition will be called with the output of the previous function, and the final result will be returned.

Here's an example implementation of the `compose` function:

```cpp
template <typename Func>
auto compose(Func&& func)
{
    return std::forward<Func>(func);
}

template <typename Func, typename... Funcs>
auto compose(Func&& func, Funcs&&... funcs)
{
    return [func, funcs...](auto&&... args) {
        return func(compose(funcs...)(std::forward<decltype(args)>(args)...));
    };
}
```

In the example above, we define two overloads of the `compose` function. The first overload handles the base case where only one function is passed as an argument. It simply returns that function.

The second overload handles the recursive case where multiple functions are passed as arguments. It creates a lambda function that calls the first function with the output of the composed result of the remaining functions. The recursive call to `compose` is responsible for handling the remaining functions.

## Using the compose Function

Once we have implemented the `compose` function, we can use it to combine functions together in a type-safe manner. Let's see an example of how to use it:

```cpp
std::string to_uppercase(const std::string& str)
{
    std::string result = str;
    std::transform(result.begin(), result.end(), result.begin(), ::toupper);
    return result;
}

std::string remove_whitespace(const std::string& str)
{
    std::string result = str;
    result.erase(std::remove_if(result.begin(), result.end(), ::isspace), result.end());
    return result;
}

int main()
{
    auto process = compose(remove_whitespace, to_uppercase);

    std::string input = "   hello world   ";
    std::string output = process(input);

    std::cout << output << std::endl;  // Output: HELLOWORLD

    return 0;
}
```

In the example above, we define two functions `to_uppercase` and `remove_whitespace`. We then use the `compose` function to create a new function called `process` that applies both of these functions to a string input. We can then call `process` with an input string and get the desired output.

## Conclusion

In this blog post, we have seen how we can implement type-safe function composition using variadic templates in C++. The `compose` function allows us to combine multiple functions together in a type-safe manner, creating powerful and reusable code. By leveraging the flexibility of variadic templates, we can achieve elegant and efficient function composition in C++. #cplusplus #functioncomposition