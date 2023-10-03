---
layout: post
title: "Audio synthesis using FM synthesis in C++"
description: " "
date: 2023-10-03
tags: [include, include]
comments: true
share: true
---

In this blog post, we will explore the concept of audio synthesis using Frequency Modulation (FM) synthesis in C++. FM synthesis is a powerful technique widely used in sound synthesis and music production. It involves modulating the frequency of one oscillating waveform (the carrier) with another oscillating waveform (the modulator).

## What is FM Synthesis?

FM synthesis creates complex timbres by varying the frequency of a simple waveform using another waveform with a different frequency. This process generates a rich and dynamic sound. The modulating waveform determines how the carrier waveform changes over time, offering a broad range of sonic possibilities.

## Setting Up the Project

To get started, let's create a new C++ project and set up the necessary libraries. We'll use the [PortAudio](http://portaudio.com) library for audio I/O and [RtMidi](https://github.com/thestk/rtmidi) for MIDI input.

1. Install PortAudio and RtMidi on your system.
2. Create a new C++ project in your preferred IDE.
3. Link the PortAudio and RtMidi libraries to your project.

## Generating Audio with FM Synthesis

Now that our project is set up, let's dive into generating audio using FM synthesis. For simplicity, we'll implement a basic FM synthesizer with a single carrier and modulator. We'll generate a sine wave as the carrier and adjust its frequency using a cosine wave as the modulator.

```cpp
#include <iostream>
#include <portaudio.h>
#include <cmath>

#define SAMPLE_RATE 44100
#define NUM_SECONDS 5

typedef struct {
    double frequency;
    double modIndex;
} FmSynthParameters;

int audioCallback(const void *inputBuffer, void *outputBuffer,
                  unsigned long framesPerBuffer,
                  const PaStreamCallbackTimeInfo* timeInfo,
                  PaStreamCallbackFlags statusFlags,
                  void *userData) {

    float* output = (float*)outputBuffer;
    FmSynthParameters* params = (FmSynthParameters*)userData;

    double phase = 0.0;
    double deltaPhase = 2.0 * M_PI * params->frequency / SAMPLE_RATE;

    for(unsigned long i = 0; i < framesPerBuffer; ++i) {
        double modulator = std::cos(phase * params->modIndex);
        double sample = std::sin(phase + modulator);
        
        output[i] = (float)sample;

        phase += deltaPhase;
    }

    return paContinue;
}

int main() {
    Pa_Initialize();

    PaStream* stream;
    Pa_OpenDefaultStream(&stream, 0, 1, paFloat32, SAMPLE_RATE, paFramesPerBufferUnspecified, audioCallback, nullptr);

    FmSynthParameters params;
    params.frequency = 440.0;
    params.modIndex = 20.0;

    Pa_StartStream(stream);
    Pa_Sleep(NUM_SECONDS * 1000);
    Pa_StopStream(stream);
    Pa_CloseStream(stream);

    Pa_Terminate();

    return 0;
}
```

In this example code, we have defined a struct `FmSynthParameters` to hold the frequency and modulation index values. The `audioCallback` function is called for each audio buffer, where we calculate the audio samples using the FM synthesis algorithm. The main function initializes the necessary audio stream and sets the parameters. We start and stop the audio stream with a predefined duration.

## Conclusion

FM synthesis is a powerful technique for creating a wide range of sounds and is widely used in various applications, including music production and sound design. In this blog post, we explored the basics of FM synthesis and implemented a simple FM synthesizer in C++. With the example code provided, you can experiment further and create your own unique sounds using FM synthesis.

#programming #audio #synthesis #C++