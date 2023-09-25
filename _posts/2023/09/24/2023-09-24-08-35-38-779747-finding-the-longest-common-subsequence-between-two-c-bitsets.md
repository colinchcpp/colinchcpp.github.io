---
layout: post
title: "Finding the longest common subsequence between two C++ Bitsets"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When working with bit-level operations in C++, Bitsets are a useful data structure to represent and manipulate binary sequences. In some scenarios, you may need to find the longest common subsequence between two Bitsets. This can be particularly useful in tasks like sequence alignment or DNA comparison.

In this blog post, we will explore an efficient algorithm to find the longest common subsequence between two C++ Bitsets. Let's dive in!

## Understanding the Problem
Before we delve into the solution, let's understand the problem. A common subsequence between two Bitsets is a sequence that appears in both Bitsets, but not necessarily consecutively. For example, given two Bitsets: `1001010` and `0101101`, the longest common subsequence is `01010`.

## Algorithm

To find the longest common subsequence between two Bitsets, we can use the dynamic programming approach with memoization. The algorithm can be summarized as follows:

1. Create a 2D table to store the lengths of the longest common subsequences for substrings of the two Bitsets.
2. Iterate through the Bitsets character by character and fill the table according to the following rules:
   - If the characters at the current positions match, increment the length of the common subsequence by 1.
   - If the characters don't match, take the maximum of the lengths of the common subsequences from the previous row and previous column.
3. Trace back the table from the bottom-right corner to construct the longest common subsequence.

Here's the implementation of the algorithm in C++:

```cpp
#include <iostream>
#include <bitset>
#include <vector>

std::vector<std::bitset<8>> longestCommonSubsequence(const std::bitset<8>& bs1, const std::bitset<8>& bs2) {
    int m = bs1.size();
    int n = bs2.size();
    std::vector<std::vector<int>> dp(m + 1, std::vector<int>(n + 1, 0));

    // Calculate the lengths of longest common subsequences
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (bs1[i - 1] == bs2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = std::max(dp[i][j - 1], dp[i - 1][j]);
            }
        }
    }

    // Trace back to construct the longest common subsequence
    std::vector<std::bitset<8>> lcs;
    int i = m, j = n;
    while (i > 0 && j > 0) {
        if (bs1[i - 1] == bs2[j - 1]) {
            lcs.push_back(bs1[i - 1]);
            i--;
            j--;
        } else if (dp[i - 1][j] >= dp[i][j - 1]) {
            i--;
        } else {
            j--;
        }
    }

    std::reverse(lcs.begin(), lcs.end());
    return lcs;
}

int main() {
    std::bitset<8> bs1("1001010");
    std::bitset<8> bs2("0101101");

    std::vector<std::bitset<8>> lcs = longestCommonSubsequence(bs1, bs2);

    for (auto bit : lcs) {
        std::cout << bit;
    }

    return 0;
}
```

## Conclusion

In this blog post, we have discussed an efficient algorithm to find the longest common subsequence between two C++ Bitsets. By utilizing dynamic programming with memoization, we can solve this problem in an optimized manner.

Remember that the algorithm presented here can be applied to Bitsets of any size, making it flexible to various use cases. Whether it's DNA sequencing, sequence matching, or any other application involving Bitsets, this algorithm will help you find the longest common subsequence efficiently.

So go ahead, experiment with Bitsets and explore the world of bit-level operations with confidence!

#bitsets #C++