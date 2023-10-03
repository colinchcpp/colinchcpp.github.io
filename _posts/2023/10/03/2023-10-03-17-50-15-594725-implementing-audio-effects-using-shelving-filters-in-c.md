---
layout: post
title: "Implementing audio effects using shelving filters in C++"
description: " "
date: 2023-10-03
tags: []
comments: true
share: true
---

Audio effects play a crucial role in enhancing the quality and character of audio signals. One popular type of audio effect is the shelving filter, which allows for selective amplification or attenuation of frequencies above or below a specified cutoff frequency. In this article, we will explore the concept of shelving filters and demonstrate how to implement them in C++.

## Understanding Shelving Filters

A shelving filter is a type of equalizer that modifies the amplitude of frequencies above or below a given threshold. It consists of two key components: a low-pass or high-pass filter and a gain control stage. The low-pass filter selectively attenuates or amplifies frequencies below the cutoff frequency, while the gain stage adjusts the amplitude of frequencies above the cutoff.

Shelving filters are commonly used in audio systems to adjust bass and treble levels. For example, boosting the bass frequencies can add warmth and depth to audio, while attenuating them can create a more balanced sound.

## Implementing Shelving Filters in C++

To implement shelving filters in C++, we can use the digital biquad filter design. The biquad filter is a widely used method for implementing digital filters and provides a flexible framework for designing various filter types, including shelving filters.

Here's an example code snippet demonstrating how to implement a shelving filter:

```cpp
const double PI = 3.141592653589793;

class ShelvingFilter {
private:
    double cutoffFrequency;
    double gain;
    double sampleRate;
    double a0, a1, a2, b1, b2; // Coefficients

public:
    ShelvingFilter(double cutoff, double gain, double sampleRate) {
        this->cutoffFrequency = cutoff;
        this->gain = gain;
        this->sampleRate = sampleRate;
        calculateCoefficients();
    }

    double processSample(double input) {
        double output = (a0 * input) + (a1 * x1) + (a2 * x2) - (b1 * y1) - (b2 * y2);

        x2 = x1;
        x1 = input;
        y2 = y1;
        y1 = output;

        return output;
    }

private:
    void calculateCoefficients() {
        double omega = 2.0 * PI * cutoffFrequency / sampleRate;
        double A = sqrt(pow(10.0, (gain / 20.0)));

        double alpha = sin(omega) / (2.0 * Q);

        a0 = (A + 1.0) + (A - 1.0) * cos(omega) + 2.0 * sqrt(A) * alpha;
        a1 = -2.0 * ((A - 1.0) + (A + 1.0) * cos(omega));
        a2 = (A + 1.0) + (A - 1.0) * cos(omega) - 2.0 * sqrt(A) * alpha;
        b1 = 2.0 * ((A - 1.0) - (A + 1.0) * cos(omega));
        b2 = (A + 1.0) - (A - 1.0) * cos(omega) - 2.0 * sqrt(A) * alpha;
    }
};
```

In this code, we define a `ShelvingFilter` class that takes parameters such as the cutoff frequency, gain, and sample rate. The `processSample` function applies the shelving filter to an input audio sample and returns the filtered output. The `calculateCoefficients` function calculates the filter coefficients based on the desired cutoff frequency, gain, and sample rate.

## Conclusion

Shelving filters are a powerful tool for implementing audio effects such as bass and treble adjustments. By selectively boosting or attenuating specific frequency ranges, shelving filters can significantly alter the tonal quality of audio signals. In this article, we explored the concept of shelving filters and demonstrated how to implement them using digital biquad filter design in C++. By leveraging these techniques, you can create versatile audio effects that enhance the listening experience.