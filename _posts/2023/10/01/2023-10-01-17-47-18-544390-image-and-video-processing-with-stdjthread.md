---
layout: post
title: "Image and video processing with `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

In modern computing, image and video processing have become essential tasks for various applications, such as computer vision, augmented reality, and multimedia systems. The ability to process images and videos efficiently is crucial for delivering a smooth user experience.

The introduction of C++20 brought many exciting new features to the language, including the `std::jthread` class. This class provides a convenient way to work with threads and asynchronous tasks. In this blog post, we will explore how to leverage `std::jthread` to process images and videos in parallel, allowing for faster and more responsive applications.

## Parallelizing Image Processing

When performing image processing tasks, such as filtering, resizing, or feature extraction, the individual operations can often be parallelized. By dividing the image into regions or pixels, each thread can process a separate section of the image simultaneously.

Let's consider an example where we have a grayscale image and want to apply a simple thresholding operation to it. This operation involves setting the pixel value to either black or white based on a predefined threshold. We can use `std::jthread` to divide the image into sections and process them concurrently.

```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <jthread>
#include <opencv2/opencv.hpp>

void thresholdImage(cv::Mat& image, int threshold, int startRow, int endRow) {
    for (int row = startRow; row < endRow; ++row) {
        for (int col = 0; col < image.cols; ++col) {
            image.at<uchar>(row, col) = (image.at<uchar>(row, col) > threshold) ? 255 : 0;
        }
    }
}

int main() {
    cv::Mat image = cv::imread("image.jpg", cv::IMREAD_GRAYSCALE);
    int threshold = 128;
    int numThreads = std::thread::hardware_concurrency();

    std::vector<std::jthread> threads(numThreads);
    int rowsPerThread = image.rows / numThreads;

    for (int i = 0; i < numThreads; ++i) {
        int startRow = i * rowsPerThread;
        int endRow = (i == numThreads - 1) ? image.rows : (i + 1) * rowsPerThread;
        threads[i] = std::jthread(thresholdImage, std::ref(image), threshold, startRow, endRow);
    }

    for (std::jthread& thread : threads) {
        thread.join();
    }

    cv::imshow("Thresholded Image", image);
    cv::waitKey(0);

    return 0;
}
```

In this code, we load a grayscale image using OpenCV (`cv::imread` with `cv::IMREAD_GRAYSCALE`) and define a `thresholdImage` function that performs the thresholding operation on a specific range of rows.

We determine the number of threads available on the system using `std::thread::hardware_concurrency`. We then create a vector of `std::jthread` objects to represent the threads and distribute the image rows evenly among them.

Within the loop, we create each thread by passing the `thresholdImage` function, along with the necessary arguments (`std::ref(image)`, `threshold`, `startRow`, `endRow`). The `std::jthread` constructor automatically starts the thread.

Finally, we join all the threads to ensure that we wait for their completion before displaying the thresholded image using OpenCV (`cv::imshow` and `cv::waitKey`).

## Video Processing with `std::jthread`

The same approach can be applied to video processing, where frames are processed independently. By dividing the video frames among threads, we can achieve real-time video processing and potentially improve performance.

In a similar manner to image processing, using `std::jthread` for video processing involves dividing the frames among threads and applying the desired operations to each frame independently.

```cpp
#include <iostream>
#include <vector>
#include <jthread>
#include <opencv2/opencv.hpp>

void processFrame(cv::Mat& frame, int frameId) {
    if (frame.empty()) {
        return;
    }

    // Process the frame
    // ...

    cv::imshow("Processed Frame", frame);
    cv::waitKey(1);
}

int main() {
    cv::VideoCapture video("video.mp4");
    int numThreads = std::thread::hardware_concurrency();

    std::vector<std::jthread> threads(numThreads);

    for (int i = 0; i < numThreads; ++i) {
        threads[i] = std::jthread([&](int threadId) {
            while (true) {
                cv::Mat frame;
                {
                    std::lock_guard<std::mutex> lock(videoMutex);
                    video >> frame;
                }

                processFrame(frame, threadId);
            }
        }, i);
    }

    for (std::jthread& thread : threads) {
        thread.join();
    }

    return 0;
}
```

In this video processing example, we create threads based on the available hardware concurrency, similar to the image processing example.

Inside the loop, we define a lambda function that represents each thread's work. Each thread continuously grabs frames from the video using `cv::VideoCapture` and passes them to the `processFrame` function for further processing.

The processed frames are displayed using OpenCV (`cv::imshow` and `cv::waitKey(1)`).

**With the power of `std::jthread`, we can easily parallelize image and video processing tasks, leading to faster and more efficient applications.** By exploiting the capabilities of modern CPUs, we can unlock the full potential of image and video processing algorithms.

#ImageProcessing #VideoProcessing