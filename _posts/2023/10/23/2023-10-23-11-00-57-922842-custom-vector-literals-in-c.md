---
layout: post
title: "Custom vector literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

In modern C++, vector literals allow us to initialize `std::vector` objects using a more concise and intuitive syntax. However, the standard C++ library does not provide built-in support for vector literals. In this blog post, we will explore how to create our own custom vector literals in C++.

## What are Vector Literals?

Vector literals are a way to initialize a vector object with a list of elements using a syntax similar to array literals. Instead of explicitly calling the vector's constructor and passing individual elements, we can use a shorthand syntax to define the elements directly.

For example, with vector literals, we can initialize a vector of integers like this:

```cpp
std::vector<int> numbers = {1, 2, 3, 4, 5};
```

## Creating Custom Vector Literals

To create our own custom vector literals, we can leverage user-defined literals in C++. User-defined literals allow us to define our own suffix for literals of specific types, including vectors.

Here's an example of creating a user-defined literal for `std::vector<int>`:

```cpp
#include <vector>

std::vector<int> operator"" _vec(const char* str, std::size_t size) {
    std::vector<int> result;

    // Parse the input literal string and populate the vector
    // You can customize the parsing logic according to your needs

    return result;
}
```

In the above code, we define an operator function `operator"" _vec` which takes a string literal as input and returns a `std::vector<int>`. The `_vec` suffix is the custom suffix we choose for our vector literals. The function body is where we parse the input string and populate the vector accordingly.

To use our custom vector literal, we can simply append the `_vec` suffix to our vector literals as follows:

```cpp
std::vector<int> numbers = "1 2 3 4 5"_vec;
```

Here, the string `"1 2 3 4 5"` is the vector literal, and the suffix `_vec` indicates that it should be interpreted as a `std::vector<int>` object.

## Example Implementation

Let's provide a concrete implementation of the parsing logic in our operator function. In this example, we will use space-separated numbers as our vector literal format. We will parse the input string and populate the vector accordingly:

```cpp
#include <vector>
#include <sstream>
#include <string>

std::vector<int> operator"" _vec(const char* str, std::size_t size) {
    std::vector<int> result;
    std::istringstream iss(std::string(str, size));

    int number;
    while (iss >> number) {
        result.push_back(number);
    }

    return result;
}
```

With this implementation, we can now use our custom vector literal syntax to initialize vectors with space-separated numbers:

```cpp
std::vector<int> numbers = "1 2 3 4 5"_vec;
```

## Conclusion

Custom vector literals provide a convenient way to initialize `std::vector` objects with a concise and intuitive syntax. By leveraging user-defined literals in C++, we can create our own custom suffixes and parsing logic to support vector literals. This allows for more readable and expressive code when working with vectors in C++.

Now that you have learned how to create custom vector literals, you can explore other variations and customization options based on your specific use cases.

#References
- [CPPReference - User-defined literals](https://en.cppreference.com/w/cpp/language/user_literal)