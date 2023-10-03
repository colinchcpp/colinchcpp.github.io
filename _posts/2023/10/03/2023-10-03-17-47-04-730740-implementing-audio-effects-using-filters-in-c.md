---
layout: post
title: "Implementing audio effects using filters in C++"
description: " "
date: 2023-10-03
tags: [include, include]
comments: true
share: true
---

## Introduction

Audio effects are an integral part of audio processing applications. They enhance the sound by modifying certain characteristics like timbre, pitch, or amplitude. One common technique for implementing audio effects is using filters. Filters allow us to manipulate the frequency content of the audio signal.

In this blog post, we will explore how to implement audio effects using filters in C++. We will discuss different types of filters and provide code examples for each.

## Types of Filters

### 1. Low-pass Filter

A low-pass filter allows frequencies below a certain cutoff frequency to pass through and attenuates frequencies above it. This filter is commonly used for effects like bass boost and noise reduction.

```cpp
#include <iostream>
#include <cmath>

#define SAMPLE_RATE 44100
#define CUTOFF_FREQUENCY 1000

double LowPassFilter(double input, double prevOutput)
{
    double RC = 1.0 / (2.0 * M_PI * CUTOFF_FREQUENCY);
    double alpha = 1.0 / (1.0 + RC / SAMPLE_RATE);
    
    // Apply low-pass filter equation
    double output = alpha * input + (1.0 - alpha) * prevOutput;
    
    return output;
}

int main()
{
    // Input audio samples
    double inputSamples[] = {0.2, 0.4, 0.8, 0.6, 0.3};
    
    // Apply low-pass filter to each sample
    double prevOutput = 0.0;
    for (int i = 0; i < sizeof(inputSamples) / sizeof(double); i++)
    {
        double output = LowPassFilter(inputSamples[i], prevOutput);
        std::cout << output << std::endl;
        prevOutput = output;
    }
    
    return 0;
}
```

### 2. High-pass Filter

A high-pass filter allows frequencies above a certain cutoff frequency to pass through and attenuates frequencies below it. It is commonly used for effects like treble boost and removing low-frequency noise.

```cpp
#include <iostream>
#include <cmath>

#define SAMPLE_RATE 44100
#define CUTOFF_FREQUENCY 1000

double HighPassFilter(double input, double prevInput, double prevOutput)
{
    double RC = 1.0 / (2.0 * M_PI * CUTOFF_FREQUENCY);
    double alpha = RC / (RC + SAMPLE_RATE);
    
    // Apply high-pass filter equation
    double output = alpha * (prevOutput + input - prevInput);
    
    return output;
}

int main()
{
    // Input audio samples
    double inputSamples[] = {0.2, 0.4, 0.8, 0.6, 0.3};
    
    // Apply high-pass filter to each sample
    double prevInput = 0.0;
    double prevOutput = 0.0;
    for (int i = 0; i < sizeof(inputSamples) / sizeof(double); i++)
    {
        double output = HighPassFilter(inputSamples[i], prevInput, prevOutput);
        std::cout << output << std::endl;
        prevInput = inputSamples[i];
        prevOutput = output;
    }
    
    return 0;
}
```

## Conclusion

Implementing audio effects using filters can significantly enhance the listening experience. In this blog post, we learned about low-pass and high-pass filters and provided code examples in C++. Feel free to explore different filter designs and experiment with different cutoff frequencies to achieve your desired audio effects.

#audioeffects #filters #audiosignalprocessing