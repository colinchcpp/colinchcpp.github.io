---
layout: post
title: "Implementing audio effects using band-pass filters in C++"
description: " "
date: 2023-10-03
tags: [include, include]
comments: true
share: true
---

Audio effects are an essential part of music production and sound engineering. One common audio effect used to shape the frequency content of a signal is the band-pass filter. In this blog post, we will explore how to implement band-pass filters in C++ to apply audio effects.

## What is a Band-Pass Filter?

A band-pass filter allows a specific range of frequencies to pass through while attenuating frequencies outside that range. This effect is often used to isolate or emphasize specific frequency components in an audio signal.

## Implementing a Band-Pass Filter

To implement a band-pass filter in C++, we can use digital signal processing algorithms. In this example, we will use the **Biquad filter** algorithm, which is widely used in audio applications:

```cpp
#include <cmath>

// Constants
const double PI = 3.141592653589793;

// BiquadCoeff struct holds the coefficients for a biquad filter
struct BiquadCoeff {
    double b0, b1, b2, a0, a1, a2;
};

// Function to calculate the coefficients for a band-pass filter
BiquadCoeff calculateBandPassCoeff(double sampleRate, double centerFreq, double Q) {
    BiquadCoeff coeff;

    double w0 = 2 * PI * centerFreq / sampleRate;
    double alpha = sin(w0) / (2 * Q);

    coeff.b0 = alpha;
    coeff.b1 = 0;
    coeff.b2 = -alpha;
    coeff.a0 = 1 + alpha;
    coeff.a1 = -2 * cos(w0);
    coeff.a2 = 1 - alpha;

    return coeff;
}
```

The `calculateBandPassCoeff` function calculates the filter coefficients required to implement a band-pass filter. It takes in the **sample rate**, **center frequency**, and **Q factor** as parameters. The function returns a `BiquadCoeff` struct that contains the calculated coefficients for the filter.

## Applying the Band-Pass Filter

Once we have the filter coefficients, we can apply the band-pass filter to an audio signal. Here's an example of how to do it:

```cpp
#include <vector>

// Function to apply the band-pass filter to an audio signal
std::vector<double> applyBandPassFilter(const std::vector<double>& input, const BiquadCoeff& coeff) {
    std::vector<double> output;
    output.reserve(input.size());

    double x1 = 0, x2 = 0, y1 = 0, y2 = 0;

    for (const auto& sample : input) {
        double y = coeff.b0 * sample + coeff.b1 * x1 + coeff.b2 * x2 - coeff.a1 * y1 - coeff.a2 * y2;
        output.push_back(y);

        x2 = x1;
        x1 = sample;
        y2 = y1;
        y1 = y;
    }

    return output;
}
```

The `applyBandPassFilter` function takes in an input audio signal as a vector of doubles and the `BiquadCoeff` struct containing the filter coefficients. It applies the band-pass filter to the input signal by iteratively processing each sample and storing the filtered output in a new vector.

## Conclusion

Implementing audio effects like band-pass filters can add depth and character to your audio projects. By using the Biquad filter algorithm and the provided code examples, you can easily create your own band-pass filter in C++. Don't be afraid to experiment and tweak the parameters to achieve the desired audio effect.

#audioeffects #C++