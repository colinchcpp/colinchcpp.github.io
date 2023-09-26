---
layout: post
title: "Checking the state of a stream after input or output"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

## Checking Input Stream State

When reading from an input stream, such as `std::cin` in C++, it is crucial to check the state of the stream after each input operation. This can be done using the `fail()` or `good()` member functions of the stream.

Here's an example in C++:

```cpp
#include <iostream>

int main() {
    int value;
    std::cout << "Enter a number: ";
    std::cin >> value;

    if (std::cin.fail()) {
        std::cout << "Invalid input. Please enter a valid number.";
    } else {
        std::cout << "You entered: " << value;
    }

    return 0;
}
```

In this example, we prompt the user to enter a number and read it into the `value` variable. After that, we check if the stream's state is in a failed state using `fail()`. If it is, we let the user know that the input is invalid. Otherwise, we display the entered value.

## Checking Output Stream State

Similarly, when writing to an output stream, such as `std::cout` in C++, it is essential to verify the state of the stream after each output operation. The `fail()` or `good()` member functions can also be used here.

Let's consider an example in C++:

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ofstream outputFile("output.txt");

    if (outputFile.is_open()) {
        outputFile << "Hello, World!";

        if (outputFile.fail()) {
            std::cout << "Failed to write to output file.";
        } else {
            std::cout << "Data written to output file successfully.";
        }

        outputFile.close();
    } else {
        std::cout << "Failed to open output file.";
    }

    return 0;
}
```

In this example, we open an output file stream and write the text "Hello, World!" to it. After the write operation, we use `fail()` to check if it was successful. If the write operation fails, we display an error message. Otherwise, we confirm that the data was written successfully.

## Conclusion

Checking the state of a stream after input or output operations is necessary to ensure that the operation was successful and that the stream is in a valid state for further operations. By utilizing the `fail()` or `good()` member functions, you can handle errors and provide appropriate feedback to the user. Implementing these checks can help to create more robust and reliable code.

#programming #stream #input #output