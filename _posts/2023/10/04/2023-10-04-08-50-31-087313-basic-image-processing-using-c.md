---
layout: post
title: "Basic image processing using C++"
description: " "
date: 2023-10-04
tags: [introduction), reading]
comments: true
share: true
---

Image processing is a widely used technique in various fields, including computer vision, medical imaging, and digital photography. In this blog post, we'll explore some basic image processing operations using C++. We'll cover operations like reading and saving images, applying filters, and converting between different color spaces.

## Table of Contents

1. [Introduction](#introduction)
2. [Reading and Saving Images](#reading-and-saving-images)
3. [Applying Filters](#applying-filters)
4. [Converting Color Spaces](#converting-color-spaces)
5. [Conclusion](#conclusion)

## Introduction

Image processing involves manipulating the pixels of an image to enhance or extract useful information. This can be achieved by applying various mathematical operations and algorithms to the pixel values.

For this tutorial, we'll use the OpenCV library, which provides a comprehensive set of functions for image processing in C++. You can install OpenCV using package managers like apt-get or manually compile and install from the source code.

## Reading and Saving Images

To start with image processing, we need to read an image from a file and save the processed image back to a file. OpenCV provides simple functions for reading and saving images. Let's see how to do that.

```cpp
#include <opencv2/opencv.hpp>

int main() {
    // Load the input image
    cv::Mat image = cv::imread("input.jpg");

    // Check if the image was successfully loaded
    if (image.empty()) {
        std::cout << "Could not open or find the image" << std::endl;
        return -1;
    }

    // Perform image processing operations here...

    // Save the processed image
    cv::imwrite("output.jpg", image);

    return 0;
}
```

In the above code, we use the `imread()` function to read an image from a file. We then check if the image was successfully loaded using the `empty()` function. After performing the desired image processing operations, we save the processed image using the `imwrite()` function.

## Applying Filters

Filters are widely used in image processing to perform operations like blurring, sharpening, edge detection, etc. OpenCV provides functions to apply various filters to an image.

Let's see an example of applying a Gaussian blur filter to an image:

```cpp
#include <opencv2/opencv.hpp>

int main() {
    cv::Mat image = cv::imread("input.jpg");

    if (image.empty()) {
        std::cout << "Could not open or find the image" << std::endl;
        return -1;
    }

    // Apply a Gaussian blur filter with a kernel size of 5x5
    cv::GaussianBlur(image, image, cv::Size(5, 5), 0);

    cv::imwrite("output.jpg", image);

    return 0;
}
```

In the above code, we use the `GaussianBlur()` function to apply a Gaussian blur filter to the image. The second and third parameters specify the input and output images, respectively. The fourth parameter is the kernel size, which determines the extent of blurring.

## Converting Color Spaces

OpenCV supports various color spaces like RGB, HSL, HSV, etc. Converting between different color spaces can be useful for different image processing tasks.

Let's see an example of converting an image from RGB to grayscale:

```cpp
#include <opencv2/opencv.hpp>

int main() {
    cv::Mat image = cv::imread("input.jpg");

    if (image.empty()) {
        std::cout << "Could not open or find the image" << std::endl;
        return -1;
    }

    // Convert the image from RGB to grayscale
    cv::cvtColor(image, image, cv::COLOR_BGR2GRAY);

    cv::imwrite("output.jpg", image);

    return 0;
}
```

In the above code, we use the `cvtColor()` function to convert the image from BGR (the default color space in OpenCV) to grayscale. The second and third parameters specify the input and output images, respectively. The fourth parameter is the conversion code (`COLOR_BGR2GRAY` in this case).

## Conclusion

In this blog post, we have explored some basic image processing techniques using C++ and the OpenCV library. We covered operations like reading and saving images, applying filters, and converting between different color spaces. However, image processing is a vast field with many more advanced techniques and algorithms. Feel free to explore further and experiment with different operations to enhance and manipulate images.

Remember to import the OpenCV library (`#include <opencv2/opencv.hpp>`) and link the necessary libraries while compiling your program.

#programming #opencv