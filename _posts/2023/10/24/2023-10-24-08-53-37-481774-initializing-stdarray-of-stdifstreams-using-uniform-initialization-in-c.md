---
layout: post
title: "Initializing std::array of std::ifstreams using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Here's an example of how you can initialize a `std::array` of `std::ifstreams` using uniform initialization:

```cpp
#include <array>
#include <fstream>

int main() {
    std::array<std::ifstream, 3> fileStreams{
        std::ifstream("file1.txt"),
        std::ifstream("file2.txt"),
        std::ifstream("file3.txt")
    };

    // Accessing and using the file streams
    for (const auto& fileStream : fileStreams) {
        if (fileStream.is_open()) {
            // Perform operations on the file stream
            // ...
        } else {
            // Handle error when opening the file
            // ...
        }
    }

    return 0;
}
```

In this example, we declare a `std::array` named `fileStreams` with a size of 3. We use uniform initialization to provide three `std::ifstream` objects, each initialized with the filenames "file1.txt", "file2.txt", and "file3.txt" respectively.

After initializing the `std::array`, you can access and use the `std::ifstream` objects as usual. In the provided `for` loop, we demonstrate how to iterate over the file streams and perform operations on each one.

Remember to include the `<array>` and `<fstream>` headers to use `std::array` and `std::ifstream`. Also, make sure to handle error cases when opening the files.

If you need different or more file streams, you can adjust the size of the `std::array` accordingly and provide additional `std::ifstream` objects in the initialization list.

I hope this helps you initialize a `std::array` of `std::ifstreams` using uniform initialization in C++!