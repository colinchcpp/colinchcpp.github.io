---
layout: post
title: "Reading and writing audio files in C++"
description: " "
date: 2023-10-03
tags: [include, include]
comments: true
share: true
---

Working with audio files is a common task in many applications, especially those related to audio processing, music production, or sound engineering. In this article, we will explore how to read and write audio files in C++.

### Reading Audio Files

To read an audio file in C++, we need to use a library such as [libsndfile](http://www.mega-nerd.com/libsndfile/) or [libsndfile-1.0.31](https://github.com/erikd/libsndfile). Here's an example of how to read a WAV file using libsndfile:

```cpp
#include <iostream>
#include <sndfile.h>

int main() {
    const char* filename = "audio.wav";
    SF_INFO file_info;           // Struct to hold file info
    SNDFILE* snd_file = nullptr;  // Pointer to sound file

    // Open the audio file for reading
    snd_file = sf_open(filename, SFM_READ, &file_info);
    if (!snd_file) {
        std::cerr << "Error opening file: " << sf_strerror(snd_file) << std::endl;
        return 1;
    }

    // Read the audio data
    int num_frames = file_info.frames;
    int num_channels = file_info.channels;
    float* audio_data = new float[num_frames * num_channels];
    sf_readf_float(snd_file, audio_data, num_frames);

    // Close the audio file
    sf_close(snd_file);

    // Process the audio data...

    delete[] audio_data;

    return 0;
}
```

In this example, we first include the necessary headers and declare the required variables. We open the audio file using `sf_open()` and check for any errors. Then, we read the audio data into a buffer using `sf_readf_float()`, which reads the audio frames into a floating point buffer. Finally, we close the audio file using `sf_close()`.

### Writing Audio Files

To write an audio file in C++, we can also use the same libraries mentioned above. Here's an example of how to write audio data into a WAV file using libsndfile:

```cpp
#include <iostream>
#include <sndfile.h>

int main() {
    const char* filename = "output.wav";
    SF_INFO file_info;           // Struct to hold file info
    SNDFILE* snd_file = nullptr;  // Pointer to sound file

    // Set the file info
    file_info.format = SF_FORMAT_WAV | SF_FORMAT_FLOAT;
    file_info.channels = 2;
    file_info.samplerate = 44100;

    // Create the audio data to write
    int num_frames = 44100;  // Assuming 1 second of audio
    int num_channels = file_info.channels;
    float* audio_data = new float[num_frames * num_channels];

    // Fill the audio data with your desired sound

    // Open the audio file for writing
    snd_file = sf_open(filename, SFM_WRITE, &file_info);
    if (!snd_file) {
        std::cerr << "Error opening file: " << sf_strerror(snd_file) << std::endl;
        return 1;
    }

    // Write the audio data
    sf_writef_float(snd_file, audio_data, num_frames);

    // Close the audio file
    sf_close(snd_file);

    delete[] audio_data;

    return 0;
}
```

In this example, we declare the necessary variables and set the file info by specifying the desired format, number of channels, and sample rate. We then create the audio data that we want to write into the file. After opening the audio file using `sf_open()`, we write the audio data using `sf_writef_float()`. Finally, we close the audio file using `sf_close()`.

By using libraries like libsndfile, you can easily read and write audio files in C++ for your audio processing applications. Remember to link the necessary libraries and handle errors appropriately to build robust audio file handling functionalities.

#programming #audio