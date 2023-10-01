---
layout: post
title: "Implementing parallel data clustering with `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

Data clustering is a common technique used in various fields such as machine learning, data analysis, and pattern recognition. It involves grouping similar data points together to discover underlying patterns or structures.

In this blog post, we will explore how to implement parallel data clustering using the C++ `std::jthread` class from the Concurrency TS. `std::jthread` provides a high-level interface for managing threads in C++.

## What is `std::jthread`?

`std::jthread` is a new addition to the C++ standard library, introduced with the Concurrency TS. It is an RAII-based thread management class that simplifies the creation, joining, and interruption of threads.

Using `std::jthread`, we can easily create parallel versions of algorithms that can take advantage of multi-core processors. This allows us to speed up computationally intensive tasks like data clustering.

## Parallel Data Clustering

To demonstrate parallel data clustering, let's consider the k-means clustering algorithm. The k-means algorithm aims to partition a dataset into k clusters, where each data point belongs to the nearest cluster mean.

Here's an example implementation of k-means clustering using `std::jthread`:

```cpp
#include <iostream>
#include <vector>
#include <thread>
#include <cmath>
#include <random>
#include <cassert>
#include <numeric>
#include <algorithm>
#include <execution>

// Compute Euclidean distance between two data points
double distance(const std::vector<double>& pointA, const std::vector<double>& pointB) {
    assert(pointA.size() == pointB.size());
    
    double sum = 0.0;
    for (size_t i = 0; i < pointA.size(); ++i) {
        double diff = pointA[i] - pointB[i];
        sum += diff * diff;
    }
    
    return std::sqrt(sum);
}

// Find the nearest cluster mean for a given point
int findNearestCluster(const std::vector<std::vector<double>>& clusters, const std::vector<double>& point) {
    int nearestCluster = 0;
    double minDistance = std::numeric_limits<double>::max();
    
    for (size_t i = 0; i < clusters.size(); ++i) {
        double dist = distance(clusters[i], point);
        if (dist < minDistance) {
            minDistance = dist;
            nearestCluster = i;
        }
    }
    
    return nearestCluster;
}

// Update cluster means based on current assignments
std::vector<std::vector<double>> updateClusterMeans(const std::vector<std::vector<double>>& data, const std::vector<int>& assignments, int numClusters) {
    std::vector<std::vector<double>> clusters(numClusters, std::vector<double>(data[0].size(), 0.0));
    std::vector<int> clusterCounts(numClusters, 0);
    
    for (size_t i = 0; i < data.size(); ++i) {
        int cluster = assignments[i];
        clusterCounts[cluster]++;
        
        for (size_t j = 0; j < data[i].size(); ++j) {
            clusters[cluster][j] += data[i][j];
        }
    }
    
    for (size_t i = 0; i < clusters.size(); ++i) {
        if (clusterCounts[i] > 0) {
            for (size_t j = 0; j < clusters[i].size(); ++j) {
                clusters[i][j] /= clusterCounts[i];
            }
        }
    }
    
    return clusters;
}

// Perform k-means clustering in parallel
std::vector<int> parallelKMeans(const std::vector<std::vector<double>>& data, int numClusters) {
    std::vector<std::vector<double>> clusters(numClusters);

    // Randomly initialize cluster means
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dist(0, data.size() - 1);
    for (auto& cluster : clusters) {
        size_t randomIndex = dist(gen);
        cluster = data[randomIndex];
    }

    std::vector<int> assignments(data.size());

    for (int iter = 0; iter < 100; ++iter) {
        // Assign each data point to the nearest cluster
        std::for_each(std::execution::par, data.begin(), data.end(), [&](const std::vector<double>& point) {
            int nearestCluster = findNearestCluster(clusters, point);
            assignments[&point - &data[0]] = nearestCluster;
        });

        // Update cluster means
        clusters = updateClusterMeans(data, assignments, numClusters);
    }

    return assignments;
}

int main() {
    // Generate random data points
    std::random_device rd;
    std::mt19937 gen(rd());
    std::normal_distribution<> dist(0.0, 1.0);

    std::vector<std::vector<double>> data(1000, std::vector<double>(2));
    for (auto& point : data) {
        for (auto& coord : point) {
            coord = dist(gen);
        }
    }

    // Perform parallel k-means clustering
    std::vector<int> assignments = parallelKMeans(data, 3);

    // Print cluster assignments
    std::cout << "Cluster assignments:\n";
    for (size_t i = 0; i < assignments.size(); ++i) {
        std::cout << assignments[i] << " ";
    }
    std::cout << "\n";

    return 0;
}
```

In this example, we first define helper functions for computing the distance between data points, finding the nearest cluster for a given point, and updating cluster means.

The `parallelKMeans` function performs k-means clustering in parallel using `std::jthread`. It initializes cluster means randomly, assigns each data point to the nearest cluster, and updates cluster means iteratively for a fixed number of iterations.

Finally, we generate random data points and perform parallel k-means clustering with three clusters. The cluster assignments are printed to standard output.

By utilizing `std::jthread`, we can easily parallelize computationally intensive tasks like data clustering. This allows us to take advantage of multi-core processors and significantly speed up the clustering process.

Give it a try and experiment with different datasets and values of `k` to see the effectiveness and efficiency of parallel data clustering!

#dataclustering #parallelcomputing