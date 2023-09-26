---
layout: post
title: "Using the std::getline function to read entire lines"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

Keywords: std::getline function, reading lines, C++, text input, string handling

---

In C++, the `std::getline` function allows you to read entire lines of text from an input stream. It is a versatile and commonly used function, especially when it comes to handling user input or reading from text files. In this blog post, we will explore how to use the `std::getline` function effectively in your C++ programs.

## Understanding the std::getline Function

The `std::getline` function is part of the `<string>` header in C++. It takes an input stream (`std::istream`) and a string as its arguments, and reads characters from the input stream until a delimiter character is encountered. By default, the delimiter is the newline character (`'\n'`).

Here's the syntax for using `std::getline`:

```cpp
std::getline(std::istream& input_stream, std::string& line_string, char delimiter = '\n');
```

- `input_stream`: The input stream from which the line will be read.
- `line_string`: A string in which the read line will be stored.
- `delimiter`: (Optional) The character that acts as the delimiter for the end of each line. The default value is the newline character (`'\n'`).

## Example Usage of std::getline

Let's consider an example where we want to read multiple lines of text from the standard input and store them in a vector. Here's how we can accomplish this using the `std::getline` function:

```cpp
#include <iostream>
#include <string>
#include <vector>

int main() {
    std::vector<std::string> lines;
    std::string input_line;

    while (std::getline(std::cin, input_line)) {
        lines.push_back(input_line);
    }

    // Print the stored lines
    for (const auto& line : lines) {
        std::cout << line << std::endl;
    }

    return 0;
}
```

In the above code, we create a vector called `lines` to store the read lines as strings. Inside the `while` loop, we use `std::getline` to read each line from `std::cin` (the standard input stream) and push it into the `lines` vector. The loop continues until there are no more lines to read.

Finally, we iterate over the `lines` vector and print each stored line using `std::cout`.

## Conclusion

The `std::getline` function in C++ is a powerful tool for reading entire lines of text from input streams. Understanding its usage and incorporating it into your programs will enable you to handle user input and process text files more efficiently. So go ahead and make use of this function to enhance your C++ programs.

#C++ #stdgetline #stringhandling #textinput