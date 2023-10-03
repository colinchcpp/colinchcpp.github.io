---
layout: post
title: "Implementing audio effects using peaking filters in C++"
description: " "
date: 2023-10-03
tags: [include, include]
comments: true
share: true
---

In this blog post, we will explore how to implement audio effects using peaking filters in C++. Peaking filters are commonly used in audio processing to boost or attenuate a specific range of frequencies. They are widely used in equalizers and audio effects such as chorus, phaser, and wah-wah pedals.

## What is a peaking filter?

A peaking filter is a type of IIR (Infinite Impulse Response) filter that modifies the amplitude of a certain range of frequencies. Unlike other types of filters that have a fixed cutoff frequency, peaking filters allow you to specify the center frequency, bandwidth, and gain.

## How to implement a peaking filter in C++

To implement a peaking filter in C++, you will need a basic understanding of digital signal processing and knowledge of the filter design techniques. Here's an example code snippet that demonstrates how to implement a peaking filter using the Direct Form II Transposed structure:

```cpp
#include <iostream>
#include <cmath>

// Peaking filter parameters
float centerFrequency = 1000.0; // in Hz
float gain = 6.0; // in dB
float bandwidth = 1.0; // in octaves

// Audio processing function
float processAudioSample(float inputSample)
{
    // Convert gain in dB to linear scale
    float gainLinear = std::pow(10.0f, gain / 20.0f);

    // Calculate filter coefficients
    float w0 = 2.0f * M_PI * centerFrequency;
    float A = std::pow(10.0f, gain / 40.0f);
    float alpha = std::sin(w0) / (2.0f * bandwidth);
    float cosw0 = std::cos(w0);

    // Calculate b0, b1, b2, a1, a2 coefficients
    float b0 = 1.0f + alpha * A;
    float b1 = -2.0f * cosw0;
    float b2 = 1.0f - alpha * A;
    float a0 = 1.0f + alpha / A;
    float a1 = -2.0f * cosw0;
    float a2 = 1.0f - alpha / A;

    // Process the audio sample
    float outputSample = inputSample * b0 + b1 * processAudioSample.prevInputSample + b2 * processAudioSample.prevPrevInputSample 
                        - a1 * processAudioSample.prevOutputSample - a2 * processAudioSample.prevPrevOutputSample;

    // Update the state variables
    processAudioSample.prevPrevInputSample = processAudioSample.prevInputSample;
    processAudioSample.prevInputSample = inputSample;
    processAudioSample.prevPrevOutputSample = processAudioSample.prevOutputSample;
    processAudioSample.prevOutputSample = outputSample;

    return outputSample;
}

int main()
{
    // Test the peaking filter
    float inputSample = 0.5f; // Input audio sample

    float outputSample = processAudioSample(inputSample);

    // Print the output sample
    std::cout << "Output sample: " << outputSample << std::endl;

    return 0;
}
```

## Conclusion

Implementing audio effects using peaking filters can greatly enhance the sound quality and allow you to shape the tone in a precise manner. In this blog post, we have learned how to implement a peaking filter in C++ using the Direct Form II Transposed structure. You can further customize the peaking filter by adjusting the center frequency, gain, and bandwidth parameters. So go ahead and experiment with different settings to create your own unique audio effects!

#audioeffects #cplusplus