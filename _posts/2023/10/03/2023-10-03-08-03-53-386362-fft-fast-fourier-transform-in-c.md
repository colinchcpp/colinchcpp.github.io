---
layout: post
title: "FFT (Fast Fourier Transform) in C++"
description: " "
date: 2023-10-03
tags: [include, include]
comments: true
share: true
---

The Fast Fourier Transform (FFT) is an efficient algorithm for computing the discrete Fourier transform (DFT) of a sequence or a signal. It is widely used in various applications such as image processing, audio signal analysis, and data compression. In this blog post, we will explore how to implement the FFT algorithm in C++.

## Understanding the FFT Algorithm

The FFT algorithm takes a sequence of N complex numbers as input and computes their DFT in O(NlogN) time complexity. It achieves this by recursively dividing the input sequence into smaller sub-problems and recombining the intermediate results. The key idea behind the FFT is to exploit the symmetry properties of the complex exponential function.

## Implementing the FFT in C++

Here is a simple implementation of the FFT algorithm in C++:

```cpp
#include <complex>
#include <cmath>
#include <vector>

typedef std::complex<double> Complex;
typedef std::vector<Complex> Vector;

// Recursive FFT implementation
void fft(Vector& x) {
    int N = x.size();

    if (N <= 1) {
        return;
    }

    // Divide the sequence into even and odd indices
    Vector even(N / 2), odd(N / 2);
    for (int i = 0; i < N; i += 2) {
        even[i / 2] = x[i];
        odd[i / 2] = x[i + 1];
    }

    // Recursively compute FFT for the even and odd subsequences
    fft(even);
    fft(odd);

    // Combine the intermediate results
    for (int k = 0; k < N / 2; ++k) {
        Complex t = std::polar(1.0, -2 * M_PI * k / N) * odd[k];
        x[k] = even[k] + t;
        x[k + N / 2] = even[k] - t;
    }
}

// Driver function to compute FFT of a given input sequence
Vector computeFFT(const Vector& input) {
    Vector x = input;
    int N = x.size();

    // Check if the input size is a power of 2
    if ((N & (N - 1)) != 0) {
        // Pad the input sequence with zeros to the nearest power of 2
        int nextPowerOf2 = pow(2, ceil(log2(N)));
        x.resize(nextPowerOf2);
        N = nextPowerOf2;
    }

    // Perform FFT on the padded sequence
    fft(x);

    return x;
}
```

## Using the FFT Algorithm

To use the FFT algorithm, you can create a vector of complex numbers representing your input sequence and pass it to the `computeFFT` function. The function will compute and return the FFT of the input sequence.

Here's an example usage of the FFT algorithm:

```cpp
int main() {
    Vector input = {Complex(1, 0), Complex(2, 0), Complex(3, 0), Complex(4, 0)};
    Vector fftResult = computeFFT(input);

    // Print the FFT result
    for (const Complex& value : fftResult) {
        std::cout << value << " ";
    }

    return 0;
}
```

## Conclusion

The FFT algorithm is a powerful tool for computing the discrete Fourier transform efficiently. In this blog post, we explored how to implement the FFT algorithm in C++. You can now use this implementation to analyze signals, perform spectral analysis, and solve various other problems in the field of signal processing. Happy coding!

#programming #FFT #C++