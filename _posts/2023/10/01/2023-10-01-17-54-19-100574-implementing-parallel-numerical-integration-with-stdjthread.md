---
layout: post
title: "Implementing parallel numerical integration with `std::jthread`"
description: " "
date: 2023-10-01
tags: [numericalintegration, parallelcomputing]
comments: true
share: true
---

In this blog post, we will explore how to implement parallel numerical integration using the `std::jthread` class in C++. Parallelizing numerical integration can significantly improve performance, especially when dealing with large datasets or complex mathematical functions. 

Parallel computing allows us to divide the computational workload among multiple threads, enabling us to leverage the capabilities of modern multi-core processors. The `std::jthread` class, introduced in C++20, provides a high-level interface for creating and managing threads.

## The Numerical Integration Algorithm

The numerical integration algorithm we will be using is the **trapezoidal rule**. The trapezoidal rule works by approximating the area under a curve by dividing it into trapezoids of equal width. The sum of the areas of these trapezoids gives an estimation of the integral value. Here is the formula:

![Trapezoidal Rule Formula](https://wikimedia.org/api/rest_v1/media/math/render/svg/ef2b2a9949bae43bf2a10a872e6e10115ebf1b95)

Where `f(x)` is the function to be integrated, `a` and `b` are the limits of integration, and `n` is the number of subdivisions.

## Single-threaded Implementation

Before diving into the parallel implementation, let's first create a single-threaded version of the numerical integration algorithm as a basis for comparison.

```cpp
double integrate(std::function<double(double)> f, double a, double b, int n) {
    double h = (b - a) / n;
    double result = 0.0;

    for (int i = 1; i <= n; ++i) {
        double x0 = a + (i - 1) * h;
        double x1 = a + i * h;
        result += 0.5 * (f(x0) + f(x1)) * h;
    }

    return result;
}
```

In this implementation, we define the function `integrate()` that takes the integrand `f`, the limits of integration `a` and `b`, and the number of subdivisions `n`. It then computes the integral using the trapezoidal rule and returns the result.

## Parallel Implementation with std::jthread

To parallelize the numerical integration algorithm, we'll divide the range of integration into smaller subranges and assign these subranges to different threads. Each thread will independently compute the integral for its assigned subrange. We'll use `std::jthread` to create and manage the worker threads.

```cpp
double parallel_integrate(std::function<double(double)> f, double a, double b, int n) {
    const int num_threads = std::jthread::hardware_concurrency();
    double h = (b - a) / n;
    double result = 0.0;

    std::vector<std::jthread> threads(num_threads);
    std::vector<double> partial_results(num_threads, 0.0);

    for (int i = 0; i < num_threads; ++i) {
        threads[i] = std::jthread([&](std::stop_token st) {
            int subrange_size = n / num_threads;
            int subrange_start = i * subrange_size + 1;
            int subrange_end = (i == num_threads - 1) ? n : (i + 1) * subrange_size;
            double partial_result = 0.0;

            for (int j = subrange_start; j <= subrange_end && !st.stop_requested(); ++j) {
                double x0 = a + (j - 1) * h;
                double x1 = a + j * h;
                partial_result += 0.5 * (f(x0) + f(x1)) * h;
            }

            partial_results[i] = partial_result;
        });
    }

    for (auto& thread : threads) {
        thread.join();
    }

    for (const auto& partial_result : partial_results) {
        result += partial_result;
    }

    return result;
}
```

In this parallel implementation, we determine the number of threads to use by retrieving `std::jthread::hardware_concurrency()`, which returns the number of concurrent threads supported by the system.

We create a vector of `std::jthread` objects and a vector of partial results to store the computed integrals for each subrange. Each thread calculates its assigned subrange's integral, and at the end, we sum up the partial results to obtain the final result.

## Conclusion

In this blog post, we discussed how to implement parallel numerical integration using the `std::jthread` class in C++. We explored the trapezoidal rule as the numerical integration algorithm and provided implementation examples for both single-threaded and parallel versions.

Parallelizing numerical integration can significantly improve performance by distributing the computational workload among multiple threads. This approach is especially useful for large datasets or complex mathematical functions.

Implementing parallel algorithms requires careful consideration of thread safety and synchronization. The `std::jthread` class simplifies thread creation and management, allowing us to focus on parallelizing the computation.

By leveraging parallel computing techniques, you can harness the power of modern multi-core processors and achieve faster and more efficient numerical integration in your applications.

#numericalintegration #parallelcomputing