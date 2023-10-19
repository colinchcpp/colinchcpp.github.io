---
layout: post
title: "Measuring the performance of sorting algorithms using std::chrono"
description: " "
date: 2023-10-20
tags: [References]
comments: true
share: true
---

Sorting algorithms are a fundamental part of computer science and are used in various applications. When comparing different sorting algorithms, it is important to assess their performance in terms of time complexity. One way to measure the execution time of sorting algorithms in C++ is by using the `std::chrono` library.

`std::chrono` is a part of the C++ Standard Library introduced in C++11, which provides a set of classes for time-oriented programming. It offers a high-resolution clock and time points to measure the execution time of code.

Let's consider an example wherein we want to measure the performance of two different sorting algorithms: Bubble Sort and Quick Sort.

First, let's implement the Bubble Sort algorithm:

```cpp
void bubbleSort(int arr[], int size) {
  for (int i = 0; i < size - 1; ++i) {
    for (int j = 0; j < size - i - 1; ++j) {
      if (arr[j] > arr[j + 1]) {
        std::swap(arr[j], arr[j + 1]);
      }
    }
  }
}
```

Next, let's implement the Quick Sort algorithm:

```cpp
int partition(int arr[], int low, int high) {
  int pivot = arr[high];
  int i = low - 1;

  for (int j = low; j < high; ++j) {
    if (arr[j] < pivot) {
      std::swap(arr[++i], arr[j]);
    }
  }

  std::swap(arr[++i], arr[high]);
  return i;
}

void quickSort(int arr[], int low, int high) {
  if (low < high) {
    int pivot = partition(arr, low, high);
    quickSort(arr, low, pivot - 1);
    quickSort(arr, pivot + 1, high);
  }
}
```

To measure the performance of these sorting algorithms, we will need to calculate the time taken by each algorithm to sort an array of a given size.

```cpp
#include <iostream>
#include <chrono>
#include <random>

// Function to generate a random array of given size
void generateRandomArray(int arr[], int size) {
  std::random_device rd;
  std::mt19937 gen(rd());
  std::uniform_int_distribution<> dis(1, 1000);

  for (int i = 0; i < size; ++i) {
    arr[i] = dis(gen);
  }
}

int main() {
  const int size = 10000;
  int arr[size];

  // Generate a random array
  generateRandomArray(arr, size);

  // Measure the execution time of Bubble Sort
  auto start = std::chrono::high_resolution_clock::now();
  bubbleSort(arr, size);
  auto end = std::chrono::high_resolution_clock::now();

  std::chrono::duration<double> duration = end - start;
  std::cout << "Bubble Sort execution time: " << duration.count() << " seconds." << std::endl;

  // Generate a new random array
  generateRandomArray(arr, size);

  // Measure the execution time of Quick Sort
  start = std::chrono::high_resolution_clock::now();
  quickSort(arr, 0, size - 1);
  end = std::chrono::high_resolution_clock::now();

  duration = end - start;
  std::cout << "Quick Sort execution time: " << duration.count() << " seconds." << std::endl;

  return 0;
}
```

In the above code, we first generate a random array of size 10,000 using the `generateRandomArray` function. Then, we measure the execution time of the Bubble Sort algorithm by calculating the duration between the `start` and `end` time points using `std::chrono::high_resolution_clock`. Similarly, we measure the execution time of the Quick Sort algorithm.

By running the above code, you will get the execution time of each sorting algorithm in seconds.

This approach allows us to compare the performance of different sorting algorithms by measuring their execution time. However, it is important to note that execution times can vary depending on factors such as the hardware and the size of the input array.

In conclusion, `std::chrono` provides a convenient way to measure the performance of sorting algorithms in C++. It allows us to accurately measure the execution time, enabling us to analyze and compare different sorting algorithms based on their time complexity.

#References:
- [C++ Standard Library - std::chrono](https://en.cppreference.com/w/cpp/chrono)
- [Bubble Sort - GeeksforGeeks](https://www.geeksforgeeks.org/bubble-sort/)
- [Quick Sort - GeeksforGeeks](https://www.geeksforgeeks.org/quick-sort/)