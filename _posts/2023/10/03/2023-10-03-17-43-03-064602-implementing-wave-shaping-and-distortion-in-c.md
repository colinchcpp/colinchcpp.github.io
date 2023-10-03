---
layout: post
title: "Implementing wave shaping and distortion in C++"
description: " "
date: 2023-10-03
tags: [programming, audioeffects]
comments: true
share: true
---

Distortion effects are commonly used in audio processing to add grit and character to sound signals. One popular technique for achieving distortion is wave shaping, which involves altering the shape of a waveform by applying a non-linear function to it. In this blog post, we'll explore how to implement wave shaping and distortion effects in C++.

## What is Wave Shaping?

Wave shaping is the process of manipulating the shape of a waveform by selectively amplifying or attenuating different parts of the signal. This alteration can create harmonic overtones and introduce non-linear distortion, resulting in a unique and desirable sound.

## Implementing Wave Shaping in C++

To implement wave shaping in C++, we can start by defining a function that applies a non-linear transformation to the input signal. Let's use a simple soft clipping algorithm as an example:

```cpp
float softClip(float input, float threshold) {
    if (input > threshold) {
        return threshold + (input - threshold) / (1.0f + std::abs(input - threshold));
    }
    else if (input < -threshold) {
        return -threshold - (input + threshold) / (1.0f + std::abs(input + threshold));
    }
    else {
        return input;
    }
}
```

In this function, we first check if the input signal exceeds a given threshold. If it does, we apply a soft clip curve to the input signal, which gradually rounds off the peaks. If the input is within the threshold range, no distortion is applied.

## Applying Distortion

Now that we have our wave shaping function, we can apply it to an audio signal to introduce distortion. Here's an example of how to apply distortion to a mono audio buffer:

```cpp
void applyDistortion(float* buffer, int bufferSize, float distortionAmount, float threshold) {
    for (int i = 0; i < bufferSize; ++i) {
        float distortedSample = softClip(buffer[i] * distortionAmount, threshold);
        buffer[i] = distortedSample;
    }
}
```

In this function, we iterate through each sample in the buffer and apply the `softClip` function to the sample multiplied by a distortion amount. The distortion amount controls the level of distortion applied, while the threshold determines when the distortion kicks in.

## Conclusion

Wave shaping and distortion effects can significantly enhance the richness and character of audio signals. By implementing wave shaping algorithms like soft clipping in C++, you can create your own custom distortion effects for audio processing applications.

Remember to experiment with different non-linear functions and parameter settings to achieve the desired distortion characteristics. And don't forget to have fun and let your creativity flow!

#programming #audioeffects