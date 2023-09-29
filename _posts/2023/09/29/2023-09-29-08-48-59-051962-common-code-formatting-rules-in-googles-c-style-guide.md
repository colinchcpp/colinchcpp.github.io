---
layout: post
title: "Common code formatting rules in Google's C++ Style Guide."
description: " "
date: 2023-09-29
tags: [tech, coding]
comments: true
share: true
---

Google's C++ Style Guide provides guidelines and best practices for writing clean, consistent, and readable C++ code. In this blog post, we will focus on some common code formatting rules from the style guide.

## 1. Indentation

- Use **2 spaces** for indentation. Avoid using tabs.

Example:
```cpp
void myFunction() {
  if (condition) {
    // code goes here
  } else {
    // code goes here
  }
}
```

## 2. Line Length

- Limit lines to a maximum of **80 characters** for better readability.

Example:
```cpp
std::string longString = "This is a long string that should be split " +
                         "into multiple lines for better readability.";
```

## 3. Brace Placement

- Place opening braces on the same line as the declaration or control statement.
- Place closing braces on a new line, aligned vertically with the opening brace.

Example:
```cpp
void myFunction() {
  if (condition) {
    // code goes here
  } else {
    // code goes here
  }
}
```

## 4. Variable Naming

- Use **lowercase** or **lowercase_with_underscore** for variable names.

Example:
```cpp
int myVariable;
std::string my_string;
```

## 5. Commenting

- Use **//** for single line comments and **/* ... */** for multi-line comments.
- Write **comments in English**.

Example:
```cpp
// This is a single line comment.

/*
 * This is a multi-line comment.
 * It can span multiple lines.
 */
```

## 6. Blank Lines

- Use blank lines between logical sections of code to improve readability.

Example:
```cpp
void functionA() {
  // code goes here
}

void functionB() {
  // code goes here
}
```
#tech #coding #programming #C++ #styleguide