---
layout: post
title: "Initializing std::array of std::ofstreams using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

```cpp
#include <array>
#include <fstream>

int main() {
    std::array<std::ofstream, 3> fileArray{
        std::ofstream("file1.txt"),
        std::ofstream("file2.txt"),
        std::ofstream("file3.txt")
    };

    // Perform operations on the fileArray like writing data
    for (auto& file : fileArray) {
        file << "Hello, World!" << std::endl;
        file.close();
    }

    return 0;
}
```

In this example, we initialize an `std::array` named `fileArray` with a size of 3 using uniform initialization. We provide three instances of `std::ofstream` objects inside the curly braces.

Each `std::ofstream` object is initialized with a filename in the constructor. You can replace `"file1.txt"`, `"file2.txt"`, and `"file3.txt"` with the actual filenames you want to use.

After initializing the `fileArray`, you can perform operations on its elements, such as writing data to the files. In the `for` loop, we iterate over each element using a reference (`auto&`) and write `"Hello, World!"` to each file. Finally, we close each file to ensure the changes are saved.

Remember to include the necessary headers `<array>` and `<fstream>` to use `std::array` and `std::ofstream`. Also, handle any potential errors that may occur during file operations.

I hope this example helps you understand how to initialize an `std::array` of `std::ofstream` objects using uniform initialization in C++. Let me know if you have any further questions!

\#C++ #FileIO