---
layout: post
title: "Implementing audio effects using chorus in C++"
description: " "
date: 2023-10-03
tags: [audioeffects, choruseffect]
comments: true
share: true
---

![Chorus](chorus_image.jpg)

Audio effects play a crucial role in enhancing the overall experience of audio applications. One popular audio effect is the chorus effect, which adds thickness and depth to the sound. In this blog post, we'll explore how to implement a chorus effect using C++.

## What is Chorus?

Chorus is an audio effect that creates the illusion of multiple sound sources playing together. It achieves this by slightly modulating the pitch and delay of the original sound source. The result is a richer and more immersive audio experience.

## Implementing Chorus Effect

To implement the chorus effect in C++, we need to manipulate the audio samples by applying modulation to the pitch and delay parameters. Let's break down the steps:

1. **Input Audio**: First, we need an input audio buffer represented as an array of audio samples. Each sample represents the amplitude of the sound at a specific point in time.

2. **Delay and Feedback**: Create a delay buffer to store the delayed audio samples. The length of the delay buffer determines the delay time of the chorus effect. To add depth to the audio, we can apply feedback by adding a fraction of the delayed sample back into the input signal.

3. **Modulation**: Generate modulation signals to manipulate the delay and pitch parameters. For example, you can use a sine wave to create smooth and periodic variations. Apply the modulation signals to adjust the delay time and pitch of the delayed samples.

4. **Output**: Mix the input audio with the delayed and modulated audio samples to create the final output. You can control the depth and speed of the chorus effect by adjusting the modulation parameters.

## Example Code

```cpp
// Define constants
const int BUFFER_SIZE = 1024;
const double modulationFrequency = 0.2;
const double modulationDepth = 0.02;
const double delayAmount = 0.005;
const double feedbackAmount = 0.5;

// Input audio buffer
double inputBuffer[BUFFER_SIZE];

// Delay buffer
double delayBuffer[BUFFER_SIZE];

// Modulated delay time
double modulatedDelayTime;

// Modulation index
double modulationIndex = 0;

// Process audio samples
for (int i = 0; i < BUFFER_SIZE; i++) {
    // Get the current sample
    double currentSample = inputBuffer[i];

    // Add feedback to the input sample
    currentSample += feedbackAmount * delayBuffer[i];

    // Determine the modulated delay time
    modulatedDelayTime = delayAmount + modulationDepth * sin(2 * M_PI * modulationFrequency * i);

    // Calculate the index position in the delay buffer
    int indexPosition = i - (int)(BUFFER_SIZE * modulatedDelayTime + modulationIndex);

    // Wrap around the delay buffer if index position is negative
    if (indexPosition < 0) {
        indexPosition += BUFFER_SIZE;
    }

    // Get the delayed sample from the delay buffer
    double delayedSample = delayBuffer[indexPosition];

    // Update the delay buffer with the current sample
    delayBuffer[i] = currentSample;

    // Mix the input and delayed samples
    double outputSample = (currentSample + delayedSample) / 2.0;

    // Store the output sample
    outputBuffer[i] = outputSample;

    // Update the modulation index
    modulationIndex += modulationDepth;
}

```

## Conclusion

In this blog post, we explored how to implement a chorus effect using C++. By manipulating the delay time and pitch with modulation, we can create a thicker and more immersive sound experience. Understanding the principles behind audio effects like chorus empowers developers to create more engaging audio applications.

#audioeffects #choruseffect