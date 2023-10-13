---
layout: post
title: "Random number generation with the <random> library"
description: " "
date: 2023-10-13
tags: [randomnumbers]
comments: true
share: true
---

Random numbers play a crucial role in many applications, such as simulations, games, cryptography, and scientific computing. In C++, the `<random>` library provides a set of classes and functions to generate random numbers with different distributions.

To generate random numbers using the `<random>` library, follow these steps:

## Step 1: Include the `<random>` header

```cpp
#include <random>
```

## Step 2: Seed the random number generator

Before generating random numbers, we need to seed the random number generator. The seed value initializes the internal state of the generator. A common way to obtain a seed value is by using the current system time.

```cpp
std::random_device rd;
std::mt19937 generator(rd());
```

In the above code, `std::random_device` is used to obtain a non-deterministic seed value, and `std::mt19937` is a popular random number generator engine.

## Step 3: Define the distribution

Next, we need to define the distribution from which we want to generate random numbers. The `<random>` library provides various distribution classes, such as `uniform_int_distribution`, `uniform_real_distribution`, `normal_distribution`, etc.

```cpp
std::uniform_int_distribution<int> distribution(1, 100);
```

In this example, `std::uniform_int_distribution` is used to generate random integers between 1 and 100 (inclusive).

## Step 4: Generate random numbers

Finally, we can generate random numbers by calling the `operator()` on the distribution object, using the random number generator as the argument.

```cpp
int random_number = distribution(generator);
```

The `operator()` returns a random number according to the specified distribution.

## Example usage

```cpp
#include <iostream>
#include <random>

int main() {
    std::random_device rd;
    std::mt19937 generator(rd());
    std::uniform_int_distribution<int> distribution(1, 100);

    for (int i = 0; i < 10; ++i) {
        int random_number = distribution(generator);
        std::cout << random_number << " ";
    }

    std::cout << std::endl;
    return 0;
}
```

This example generates 10 random integers between 1 and 100 (inclusive) and prints them on the console.

Using the `<random>` library, you have the flexibility to generate random numbers with different distributions, such as uniform, normal, exponential, etc. Experiment with different distribution classes and parameters to suit your specific needs.

To learn more about the `<random>` library and its available functionalities, refer to the [C++ documentation](https://en.cppreference.com/w/cpp/numeric/random).

#randomnumbers #C++