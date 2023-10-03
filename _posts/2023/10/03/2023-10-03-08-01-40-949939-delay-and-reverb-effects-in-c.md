---
layout: post
title: "Delay and reverb effects in C++"
description: " "
date: 2023-10-03
tags: [programming, audioeffects]
comments: true
share: true
---

When it comes to audio effects processing, delay and reverb are two of the most commonly used effects. They can add depth, space, and ambience to audio signals, whether it's a musical recording, a podcast, or a game.

In this blog post, we will explore how to implement delay and reverb effects using C++.

## Delay Effect

The delay effect creates an echo-like sound by repeating the input signal after a certain delay period. The basic algorithm for a delay effect involves storing a buffer of the input signal and playing it back after a specified amount of time. Here's an example code snippet:

```cpp
const int bufferSize = 44100; // buffer size in samples
float buffer[bufferSize]; // buffer to store input signal

void delayEffect(float *input, float *output, int length, float delayTime, float feedback) {
    int delaySamples = int(delayTime * sampleRate); // convert delay time to samples

    for (int i = 0; i < length; i++) {
        output[i] = input[i] + feedback * buffer[i - delaySamples];
        buffer[i] = input[i];
    }
}
```

In the above code, `input` is the input signal, `output` is the output signal, `length` is the length of the signal in samples, `delayTime` is the delay time in seconds, and `feedback` controls the amount of feedback in the delay effect.

## Reverb Effect

The reverb effect simulates the acoustic properties of different spaces, such as rooms, halls, or stadiums. It adds a series of delayed and attenuated reflections to the input signal to create a sense of spaciousness. Implementing a reverb effect can be more complex compared to a delay effect, as it involves multiple delay lines and feedback loops.

Here's a simplified example code snippet that demonstrates a basic reverb effect using a simple feedback delay network (FDN):

```cpp
const int numDelayLines = 4; // number of delay lines
const float delays[numDelayLines] = {0.02, 0.035, 0.045, 0.05}; // delay times for each line
const float feedbacks[numDelayLines] = {0.5, 0.3, 0.2, 0.1}; // feedback gains for each line

float buffer[numDelayLines][bufferSize]; // buffer for each delay line

void reverbEffect(float *input, float *output, int length) {
    for (int i = 0; i < length; i++) {
        float sample = input[i];

        for (int j = 0; j < numDelayLines; j++) {
            int delaySamples = int(delays[j] * sampleRate);
            sample += feedbacks[j] * buffer[j][i - delaySamples];
            buffer[j][i] = sample;
        }

        output[i] = sample;
    }
}
```

In the code above, `delays` and `feedbacks` define the delay times and feedback gains for each delay line, respectively. The `buffer` array stores the delayed samples for each delay line.

These examples provide a starting point for implementing delay and reverb effects in C++. You can further enhance these effects by incorporating additional features such as filtering, modulation, and more complex algorithms.

Implementing audio effects in C++ allows for fine-grained control and customization, making it a popular choice for audio processing applications. Experiment with different parameters and algorithms to achieve the desired sound and explore more advanced techniques in audio effect processing.

#programming #audioeffects