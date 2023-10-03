---
layout: post
title: "Implementing audio effects using exciters in C++"
description: " "
date: 2023-10-03
tags: [include, audioeffects]
comments: true
share: true
---

In the realm of audio processing, exciters play a crucial role in enhancing the quality and character of audio signals. Exciters are commonly used in a variety of applications, including music production, audio mastering, and sound design. By introducing harmonic content and adding subtle or dramatic enhancements, exciters can make audio signals more vibrant and exciting.

In this blog post, we'll explore how to implement audio effects using exciters in C++. We'll cover the basics of exciters, their underlying principles, and provide an example code implementation to get you started.

## Understanding Exciters

An exciter is an audio effect that emphasizes specific harmonics or frequency bands of an audio signal. It works by splitting the input signal into various frequency bands and then applying harmonically-related processing to each band. The processed bands are then mixed back together to produce the final, enhanced output.

Exciters typically consist of the following modules:

1. **Splitter**: The incoming audio signal is split into multiple frequency bands using a crossover or filter bank. This allows independent processing of different parts of the frequency spectrum.

2. **Harmonic Generation**: Each frequency band is processed individually to generate additional harmonics. Techniques like distortion, saturation, or waveshaping can be applied to introduce richness and character to the audio.

3. **Mixing**: The processed bands are mixed back together, along with the original unprocessed signal, to create the final output. The mixing process must be carefully balanced to maintain the desired level of enhancement without introducing unwanted artifacts.

## Example Code Implementation

Let's take a look at a basic implementation of an exciter using C++. For simplicity, we'll focus on a single-band exciter that works on the entire frequency spectrum.

```cpp
#include <cmath>

// Exciter class definition
class Exciter {
public:
    Exciter(float drive, float mix) : drive_(drive), mix_(mix) {}

    // Process audio samples
    float processSample(float sample) {
        float dry = sample;
        float wet = std::tanh(drive_ * sample); // Harmonic generation using distortion
        return (dry * (1 - mix_)) + (wet * mix_); // Mixing dry and wet signals
    }

private:
    float drive_; // Exciter drive control
    float mix_; // Wet/dry mix control
};

// Example usage
int main() {
    const float drive = 0.5; // Exciter drive control value (0-1)
    const float mix = 0.7; // Wet/dry mix control value (0-1)

    Exciter exciter(drive, mix);

    // Process audio samples
    float inputSample = 0.5; // Example input sample
    float outputSample = exciter.processSample(inputSample);

    return 0;
}
```

In the example above, we define an `Exciter` class that takes in parameters for drive and mix controls. The `processSample` function applies distortion-based harmonic generation using the `std::tanh` function and performs the mixing of the dry and wet signals.

The example usage in the `main` function demonstrates how to create an instance of the `Exciter` class, set the drive and mix control values, and process a single audio sample.

## Conclusion

Implementing audio effects using exciters can significantly enhance the quality and character of audio signals. By understanding the underlying principles and implementing the necessary processing steps, you can create exciting and engaging audio effects in your C++ projects.

Remember, the example provided here is a basic implementation, and there are countless possibilities for extending and refining the exciter effect. Experiment with different processing techniques, frequency band splitting, and mixing strategies to create your own unique audio effects.

#audioeffects #exciters