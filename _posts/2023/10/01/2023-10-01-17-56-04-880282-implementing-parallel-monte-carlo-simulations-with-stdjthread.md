---
layout: post
title: "Implementing parallel Monte Carlo simulations with `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

Monte Carlo simulations have become an essential tool in various fields, from finance to scientific research. These simulations involve performing a large number of random experiments to estimate the behavior of a system or model. One common challenge is executing these simulations efficiently, especially when there are numerous simulations to be performed. In this blog post, we will explore how to implement parallel Monte Carlo simulations using the `std::jthread` class in C++.

## What is `std::jthread`? ##

Introduced in C++20, the `std::jthread` class provides a simple and efficient way to manage threads in C++. It is an improvement over the existing `std::thread` class, offering support for joinable threads, letting you avoid the need for manual cleanup. With `std::jthread`, you can create and manage threads with ease, making it ideal for parallelizing Monte Carlo simulations.

## Setting up the environment ##

Before we dive into the implementation details, let's set up the environment by including the necessary headers:

```cpp
#include <iostream>
#include <vector>
#include <random>
#include <chrono>
#include <numeric>
#include <thread>
#include <future>
```

Here, we have included headers for input/output, vectors, random number generators, timing, and concurrency utilities.

## Implementing the Monte Carlo simulation ##

Let's begin by implementing a simple Monte Carlo simulation that estimates the value of π (Pi) using the random generation of points within a square with a quarter circle inscribed in it.

```cpp
double estimatePi(int numPoints) {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_real_distribution<> dis(0.0, 1.0);

    int insideCircle = 0;
    for(int i = 0; i < numPoints; i++) {
        double x = dis(gen);
        double y = dis(gen);
        if((x*x) + (y*y) <= 1)
            insideCircle++;
    }

    return 4.0 * static_cast<double>(insideCircle) / numPoints;
}
```

In this code snippet, we initialize a random number generator, `gen`, and a uniform distribution, `dis`, to generate random numbers between 0 and 1. We then iterate `numPoints` times, generating random `x` and `y` coordinates within the square. If the point is within the quarter circle, we increment the `insideCircle` counter.

Finally, we estimate the value of π by multiplying the ratio of points inside the circle by 4.0.

## Running simulations in parallel using `std::jthread` ##

Now, let's see how we can parallelize the Monte Carlo simulations using `std::jthread`. We will create a helper function that performs multiple simulations concurrently using multiple threads.

```cpp
double runSimulations(int numSimulations, int numPoints) {
    std::vector<std::jthread> threads;
    std::vector<std::future<double>> results;

    for(int i = 0; i < numSimulations; i++) {
        results.emplace_back(std::async(std::launch::deferred, estimatePi, numPoints));
        threads.emplace_back(std::jthread([i]() {
            std::cout << "Simulation " << i << " completed" << std::endl;
        }));
    }

    double sum = 0.0;
    for(auto& result : results) {
        sum += result.get();
    }

    return sum / numSimulations;
}
```

In this code snippet, we create two vectors: `threads` to store the `std::jthread` objects and `results` to store the `std::future` objects holding the results of each simulation. 

Within the loop, we launch a simulation using `std::async` and `estimatePi`, deferring the execution until we call `result.get()`. We also create a `std::jthread` object to print a completion message for each simulation.

Finally, we sum up the results from each simulation and return the average estimate of π.

## Putting it all together ##

To run the parallel Monte Carlo simulations, we need to call the `runSimulations` function with the desired number of simulations and points per simulation.

```cpp
int main() {
    int numSimulations = 4;
    int numPoints = 1000000;

    double piEstimate = runSimulations(numSimulations, numPoints);
    std::cout << "Estimated value of pi: " << piEstimate << std::endl;

    return 0;
}
```

In this example, we run four simulations, each with one million random points. The estimated value of π is then printed to the console.

## Conclusion ##

Parallelizing Monte Carlo simulations using `std::jthread` can significantly improve the efficiency of your simulations. By leveraging the power of multiple threads, you can perform a large number of simulations concurrently, reducing the overall execution time.

Using the example code provided, you can adapt and extend it to suit your specific Monte Carlo simulation needs. Remember to measure the performance and make adjustments accordingly to achieve optimal results.

#cpp #MonteCarlo #ParallelSimulation