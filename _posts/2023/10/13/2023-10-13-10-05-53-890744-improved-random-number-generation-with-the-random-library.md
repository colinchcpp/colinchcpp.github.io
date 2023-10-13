---
layout: post
title: "Improved random number generation with the <random> library"
description: " "
date: 2023-10-13
tags: []
comments: true
share: true
---

In many programming applications, the need for generating random numbers is quite common. Whether it's for generating passwords, simulating events, or any other scenario that requires randomness, it's important to have a reliable and robust method for generating random numbers.

In C++, the `<random>` library provides a set of tools for generating random numbers. This library introduces improved random number generation algorithms and a more flexible and modern approach compared to the older `<cstdlib>` library.

Let's take a look at how we can use the `<random>` library to generate random numbers in C++.

## Including the random library

To start using the `<random>` library, we need to include it in our C++ program:

```cpp
#include <random>
```

## Generating random integers

The `<random>` library provides multiple random number generators, each with its own set of properties and uses. One commonly used generator is the `std::mt19937` generator, which is based on the Mersenne Twister algorithm.

To generate random integers within a specific range, we can use the `std::uniform_int_distribution` class. Here's an example of generating a random integer between 1 and 10:

```cpp
std::random_device rd;  // Obtain a random seed from the operating system
std::mt19937 gen(rd());  // Initialize the random number generator with the seed

std::uniform_int_distribution<int> dis(1, 10);  // Define the range

int random_number = dis(gen);  // Generate the random number

std::cout << "Random number: " << random_number << std::endl;
```

## Generating random floating-point numbers

Similar to generating random integers, we can also generate random floating-point numbers within a specific range using the `std::uniform_real_distribution` class. Here's an example of generating a random number between 0 and 1:

```cpp
std::random_device rd;  // Obtain a random seed from the operating system
std::mt19937 gen(rd());  // Initialize the random number generator with the seed

std::uniform_real_distribution<double> dis(0.0, 1.0);  // Define the range

double random_number = dis(gen);  // Generate the random number

std::cout << "Random number: " << random_number << std::endl;
```

## Generating random boolean values

If you need to generate random boolean values, you can utilize the `std::bernoulli_distribution` class provided by the `<random>` library. This distribution generates `true` or `false` with a specific probability. Here's an example:

```cpp
std::random_device rd;  // Obtain a random seed from the operating system
std::mt19937 gen(rd());  // Initialize the random number generator with the seed

std::bernoulli_distribution dis(0.5);  // 50% chance of getting true or false

bool random_value = dis(gen);  // Generate the random boolean value

std::cout << "Random value: " << std::boolalpha << random_value << std::endl;
```

## Conclusion

The `<random>` library in C++ provides a powerful and flexible set of tools for generating random numbers. By using the appropriate random number generator and distribution classes, you can generate random integers, floating-point numbers, and boolean values with ease and control.

Using the improved random number generation capabilities of the `<random>` library ensures more reliable and consistent randomness in your applications, making it a valuable addition to your C++ programming toolkit.

**References:**
- [C++ `<random>` - cppreference.com](https://en.cppreference.com/w/cpp/numeric/random)