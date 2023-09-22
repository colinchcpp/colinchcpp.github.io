---
layout: post
title: "Recursive templates for string manipulations in C++"
description: " "
date: 2023-09-22
tags: [tech, string]
comments: true
share: true
---

In this blog post, we'll explore how to use recursive templates in C++ to manipulate strings. Recursive templates provide a powerful way to perform various operations on strings at compile time.

## What are Recursive Templates?

Recursive templates are a technique in C++ where a templated function or class can call itself, allowing for recursion. This recursive behavior enables powerful compile-time computations.

## Using Recursive Templates for String Manipulations

Let's start by exploring a simple example: reversing a string using recursive templates.

```cpp
template <size_t N>
struct StringReverser {
    // Base case: Reverse an empty string
    static constexpr std::string_view reverse(std::string_view str) {
        return "";
    }
};

template <size_t N>
struct StringReverser {
    // Recursive case: Reverse a non-empty string
    static constexpr std::string_view reverse(std::string_view str) {
        return str.back() + StringReverser<N - 1>::reverse(str.substr(0, str.length() - 1));
    }
};
```

In this example, we define a `StringReverser` template struct with a static member function `reverse`. The base case handles an empty string, while the recursive case reverses a non-empty string by appending the last character to the reverse of the remaining substring.

To use this template, we can simply call the `reverse` function:

```cpp
const std::string_view reversed = StringReverser<5>::reverse("Hello");
std::cout << reversed << std::endl; // Output: olleH
```

## More String Manipulations with Recursive Templates

Recursive templates can be used for various string manipulations other than reversal. Here are a few examples:

### Counting Characters

```cpp
template <char C, size_t N>
struct CharacterCounter {
    // Base case: Empty string, count is zero
    static constexpr size_t count(std::string_view str) {
        return 0;
    }
};

template <char C, size_t N>
struct CharacterCounter {
    // Recursive case: Count the occurrence of character C in the string
    static constexpr size_t count(std::string_view str) {
        return (str.front() == C) + CharacterCounter<C, N - 1>::count(str.substr(1));
    }
};
```

### Removing Characters

```cpp
template <char C, size_t N>
struct CharacterRemover {
    // Base case: Empty string
    static constexpr std::string_view remove(std::string_view str) {
        return str;
    }
};

template <char C, size_t N>
struct CharacterRemover {
    // Recursive case: Remove all occurrences of character C from the string
    static constexpr std::string_view remove(std::string_view str) {
        return (str.front() == C)
            ? CharacterRemover<C, N - 1>::remove(str.substr(1))
            : str.front() + CharacterRemover<C, N - 1>::remove(str.substr(1));
    }
};
```

## Conclusion

Recursive templates in C++ provide a powerful way to perform string manipulations at compile time. By leveraging the recursive behavior of templates, you can create concise and efficient code that operates on strings. This technique opens up a world of possibilities for compile-time computations and string processing in C++.

#tech #C++ #string-manipulation #recursive-templates