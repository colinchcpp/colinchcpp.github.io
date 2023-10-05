---
layout: post
title: "Implementing image quality assessment in C++"
description: " "
date: 2023-10-04
tags: [psnr)]
comments: true
share: true
---

Image quality assessment is an important task in computer vision and image processing. It allows us to measure the perceived quality of an image, which is crucial for various applications like image compression, image enhancement, and image restoration. In this blog post, we will explore how to implement image quality assessment in C++.

## Table of Contents
1. [Introduction](#introduction)
2. [PSNR (Peak Signal-to-Noise Ratio)](#psnr)
3. [SSIM (Structural Similarity Index)](#ssim)
4. [Conclusion](#conclusion)

## Introduction
Before diving into the implementation, let's briefly discuss the two commonly used metrics for image quality assessment: PSNR and SSIM.

## PSNR (Peak Signal-to-Noise Ratio)
PSNR is a popular metric used to measure the quality of a reconstructed image by comparing it to the original image. It calculates the ratio between the maximum possible power of a signal and the power of corrupting noise that affects the quality of the image.

```cpp
#include <iostream>
#include <cmath>

double calculatePSNR(const cv::Mat& originalImage, const cv::Mat& reconstructedImage) {
  cv::Mat difference;
  cv::absdiff(originalImage, reconstructedImage, difference);
  difference.convertTo(difference, CV_32F);
  difference = difference.mul(difference);
  double meanSquaredError = cv::mean(difference).val[0];

  if (meanSquaredError <= 1e-10) {
    return 0.0; // Images are identical
  } else {
    double maxPixelValue = 255.0;
    double psnr = 10.0 * std::log10((maxPixelValue * maxPixelValue) / meanSquaredError);
    return psnr;
  }
}
```
 
## SSIM (Structural Similarity Index)
SSIM is another widely used metric that measures the structural similarity between two images. It takes into account both the luminance and contrast perception of an image. SSIM values range between -1 and 1, where values close to 1 indicate higher similarity.

```cpp
#include <iostream>
#include <opencv2/opencv.hpp>

double calculateSSIM(const cv::Mat& originalImage, const cv::Mat& reconstructedImage) {
  const double C1 = 6.5025, C2 = 58.5225;
  cv::Mat img1, img2;
  originalImage.convertTo(img1, CV_32F);
  reconstructedImage.convertTo(img2, CV_32F);

  cv::Mat img1Square, img2Square, imgMultiply;
  cv::multiply(img1, img1, img1Square);
  cv::multiply(img2, img2, img2Square);
  cv::multiply(img1, img2, imgMultiply);

  cv::Mat img1Mean, img2Mean, imgMultiplyMean;
  cv::GaussianBlur(img1, img1Mean, cv::Size(11, 11), 1.5);
  cv::GaussianBlur(img2, img2Mean, cv::Size(11, 11), 1.5);
  cv::GaussianBlur(imgMultiply, imgMultiplyMean, cv::Size(11, 11), 1.5);

  cv::Mat img1MeanSquare = img1Mean.mul(img1Mean);
  cv::Mat img2MeanSquare = img2Mean.mul(img2Mean);
  cv::Mat imgMeanMultiply = img1Mean.mul(img2Mean);

  cv::Mat img1SigmaSquare, img2SigmaSquare, imgSigmaMultiply;
  cv::subtract(img1Square, img1MeanSquare, img1SigmaSquare);
  cv::subtract(img2Square, img2MeanSquare, img2SigmaSquare);
  cv::subtract(imgMultiply, imgMeanMultiply, imgSigmaMultiply);

  cv::add(img1SigmaSquare, cv::Scalar(C1), img1SigmaSquare);
  cv::add(img2SigmaSquare, cv::Scalar(C1), img2SigmaSquare);
  cv::add(imgSigmaMultiply, cv::Scalar(C2), imgSigmaMultiply);

  cv::Mat ssimMap;
  cv::divide(imgSigmaMultiply, img1SigmaSquare + img2SigmaSquare + cv::Scalar(C2), ssimMap);

  cv::Scalar mssim = cv::mean(ssimMap);
  double ssim = (mssim.val[0] + mssim.val[1] + mssim.val[2]) / 3.0;

  return ssim;
}
```

## Conclusion
Implementing image quality assessment in C++ can provide valuable insights into the quality of an image. The examples above demonstrate two popular metrics, PSNR and SSIM, that can be used to quantify image quality. By integrating these metrics into your image processing pipeline, you can make informed decisions for various applications.

Remember to choose the appropriate metric based on the specific requirements of your project. While PSNR is widely used and straightforward to implement, SSIM takes into account more perceptual aspects of image similarity. Experimenting with different metrics can help you achieve more accurate and reliable results.

#imageprocessing #computervision