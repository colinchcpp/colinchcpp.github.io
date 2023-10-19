---
layout: post
title: "Calculating the time taken to perform compression and decompression using std::chrono"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

Compression and decompression are common tasks performed in many software applications. It's important to have an idea of how much time these operations take to optimize their efficiency. In this blog post, we will explore how to calculate the time taken to perform compression and decompression using the `std::chrono` library in C++.

## Table of Contents
- [Introduction](#introduction)
- [Compression using std::chrono](#compression-using-stdchrono)
- [Decompression using std::chrono](#decompression-using-stdchrono)
- [Conclusion](#conclusion)

## Introduction
The `std::chrono` library provides a high-resolution clock for measuring time durations in C++. We can leverage this library to accurately measure the time taken to perform compression and decompression tasks.

## Compression using std::chrono
To calculate the time taken to compress a file using `std::chrono`, we need to measure the time before and after the compression operation. Here's an example code snippet that demonstrates this:

```cpp
#include <iostream>
#include <fstream>
#include <chrono>
#include <zlib.h>

int main() {
    const std::string sourceFilename = "source.txt";
    const std::string targetFilename = "compressed.gz";

    // Measure start time
    auto startTime = std::chrono::steady_clock::now();

    // Perform compression
    std::ifstream sourceFile(sourceFilename, std::ios::binary);
    std::ofstream targetFile(targetFilename, std::ios::binary);
    gzFile compressedFile = gzopen(targetFilename.c_str(), "wb");
    char buffer[1024];
    while (sourceFile.read(buffer, sizeof(buffer)))
        gzwrite(compressedFile, buffer, sizeof(buffer));
    gzclose(compressedFile);

    // Measure end time
    auto endTime = std::chrono::steady_clock::now();

    // Calculate duration
    auto duration = std::chrono::duration_cast<std::chrono::milliseconds>(endTime - startTime);

    std::cout << "Compression took " << duration.count() << " milliseconds." << std::endl;

    return 0;
}
```

In this example, we start by opening the source and target files. We then measure the start time using `std::chrono::steady_clock::now()`. After performing the compression using zlib, we measure the end time in a similar manner. Finally, we calculate the duration by subtracting the start time from the end time and printing it.

## Decompression using std::chrono
Similar to compression, we can also measure the time taken to decompress a compressed file using `std::chrono`. Here's an example code snippet that demonstrates this:

```cpp
#include <iostream>
#include <fstream>
#include <chrono>
#include <zlib.h>

int main() {
    const std::string sourceFilename = "compressed.gz";
    const std::string targetFilename = "decompressed.txt";

    // Measure start time
    auto startTime = std::chrono::steady_clock::now();

    // Perform decompression
    gzFile compressedFile = gzopen(sourceFilename.c_str(), "rb");
    std::ofstream targetFile(targetFilename, std::ios::binary);
    char buffer[1024];
    int bytesRead;
    while ((bytesRead = gzread(compressedFile, buffer, sizeof(buffer))) > 0)
        targetFile.write(buffer, bytesRead);
    gzclose(compressedFile);

    // Measure end time
    auto endTime = std::chrono::steady_clock::now();

    // Calculate duration
    auto duration = std::chrono::duration_cast<std::chrono::milliseconds>(endTime - startTime);

    std::cout << "Decompression took " << duration.count() << " milliseconds." << std::endl;

    return 0;
}
```

In this example, we open the compressed file using `gzopen()` from zlib and the target file for writing. We measure the start time, perform decompression using `gzread()`, and write the decompressed data to the target file. Finally, we measure the end time, calculate the duration, and print it.

## Conclusion
By using `std::chrono` in C++, we can accurately measure the time taken to perform compression and decompression tasks. This information can be helpful in optimizing the efficiency of these operations. Remember to include the necessary libraries and follow the proper file handling procedures when working with compression and decompression tasks.

# References
- [std::chrono - C++ Reference](https://en.cppreference.com/w/cpp/chrono)
- [zlib - A Massively Spiffy Yet Delicately Unobtrusive Compression Library](https://www.zlib.net/)