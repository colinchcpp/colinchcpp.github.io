---
layout: post
title: "High-frequency pairs selection algorithms using C++"
description: " "
date: 2023-09-21
tags: [algorithmictrading]
comments: true
share: true
---

In algorithmic trading, high-frequency pairs selection plays a crucial role in maximizing trading profits. By identifying and selecting pairs of assets that have a strong statistical relationship, traders can exploit these relationships to make profitable trades. In this blog post, we will explore some high-frequency pairs selection algorithms using C++.

## 1. Mean Reversion

Mean reversion is a popular strategy in pairs trading that aims to capitalize on the reversion of asset prices to their mean. The algorithm involves selecting pairs of assets that have historically moved together but have deviated from their average relationship. Here's an example implementation in C++:

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <cmath>

// Calculate mean of a given vector
double calculateMean(const std::vector<double>& data) {
    double sum = 0.0;
    for (const auto& element : data) {
        sum += element;
    }
    return sum / data.size();
}

// Calculate standard deviation of a given vector
double calculateStdDev(const std::vector<double>& data, double mean) {
    double variance = 0.0;
    for (const auto& element : data) {
        variance += std::pow(element - mean, 2);
    }
    return std::sqrt(variance / data.size());
}

// Identify pairs based on mean reversion strategy
void identifyPairsMeanReversion(const std::vector<std::vector<double>>& assetPrices) {
    for (size_t i = 0; i < assetPrices.size(); i++) {
        for (size_t j = i + 1; j < assetPrices.size(); j++) {
            double mean1 = calculateMean(assetPrices[i]);
            double mean2 = calculateMean(assetPrices[j]);
            double stdDev1 = calculateStdDev(assetPrices[i], mean1);
            double stdDev2 = calculateStdDev(assetPrices[j], mean2);
            
            // Check for mean reversion condition
            if (std::abs(mean1 - mean2) <= stdDev1 + stdDev2) {
                std::cout << "Pair: Asset" << i << ", Asset" << j << std::endl;
            }
        }
    }
}

int main() {
    // Sample asset prices data
    std::vector<std::vector<double>> assetPrices = {{10, 12, 8, 9, 11},
                                                    {9, 10, 11, 12, 13},
                                                    {8, 11, 7, 9, 10}};
    
    // Identify pairs based on mean reversion
    identifyPairsMeanReversion(assetPrices);

    return 0;
}
{% endraw %}
```

## 2. Co-Integration

Co-integration is another powerful technique used in pairs trading. It involves identifying pairs of assets that have a long-term relationship, even though their individual prices may exhibit short-term divergence. Here's an example implementation of co-integration algorithm in C++:

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <cmath>

// Calculate coefficient of determination (R-squared)
double calculateRSquared(const std::vector<double>& y1, const std::vector<double>& y2) {
    double sumXY = 0.0;
    double sumX2 = 0.0;
    double sumY2 = 0.0;
    double sumX = 0.0;
    double sumY = 0.0;
    size_t n = y1.size();

    for (size_t i = 0; i < n; i++) {
        sumXY += y1[i] * y2[i];
        sumX2 += y1[i] * y1[i];
        sumY2 += y2[i] * y2[i];
        sumX += y1[i];
        sumY += y2[i];
    }

    double numerator = n * sumXY - sumX * sumY;
    double denominator = std::sqrt((n * sumX2 - sumX * sumX) * (n * sumY2 - sumY * sumY));
    
    return std::pow(numerator / denominator, 2);
}

// Identify pairs based on co-integration strategy
void identifyPairsCoIntegration(const std::vector<std::vector<double>>& assetPrices) {
    size_t n = assetPrices.size();
    std::vector<double> rSquaredValues(n * (n - 1) / 2, 0.0);
    
    size_t count = 0;
    for (size_t i = 0; i < n; i++) {
        for (size_t j = i + 1; j < n; j++) {
            double rSquared = calculateRSquared(assetPrices[i], assetPrices[j]);
            rSquaredValues[count++] = rSquared;
        }
    }
    
    double threshold = 0.5; // R-squared threshold for co-integration
    count = 0;
    for (size_t i = 0; i < n; i++) {
        for (size_t j = i + 1; j < n; j++) {
            if (rSquaredValues[count++] > threshold) {
                std::cout << "Pair: Asset" << i << ", Asset" << j << std::endl;
            }
        }
    }
}

int main() {
    // Sample asset prices data
    std::vector<std::vector<double>> assetPrices = {{10, 12, 8, 9, 11},
                                                    {9, 10, 11, 12, 13},
                                                    {8, 11, 7, 9, 10}};
    
    // Identify pairs based on co-integration
    identifyPairsCoIntegration(assetPrices);

    return 0;
}
{% endraw %}
```

## Conclusion

High-frequency pairs selection algorithms can help traders identify profitable trading opportunities in algorithmic trading. Mean reversion and co-integration are two commonly used strategies for selecting pairs of assets. By implementing these algorithms in C++, traders can efficiently analyze asset price data and make informed trading decisions.

\#algorithmictrading #CPP