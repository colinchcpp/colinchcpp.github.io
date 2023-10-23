---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting elements is a common task in programming, and most programming languages provide built-in sorting functions or libraries to accomplish this. In C++, the `std::sort()` function from the `<algorithm>` library is often used for sorting.

By default, the `std::sort()` function uses the `<` operator to determine the order of elements. However, there might be cases where you need to customize the sorting logic for certain data types or situations. In this blog post, we will explore how to perform custom sorting using literals in C++.

Let's consider a scenario where we have a vector of strings representing book titles. We want to sort the titles alphabetically, but with a specific ordering for certain special keywords.

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

bool compareTitles(const string& title1, const string& title2) {
    // Compare logic
}

int main() {
    vector<string> titles = {"The Great Gatsby", "Harry Potter", "A Song of Ice and Fire", "Lord of the Rings"};

    sort(titles.begin(), titles.end(), compareTitles);

    for (const auto& title : titles) {
        cout << title << endl;
    }

    return 0;
}
```

In the above code, we have defined a `compareTitles()` function that takes two strings and compares them based on our custom logic. This function will be used as the comparison function for the `std::sort()` algorithm.

To implement our custom sorting logic, we can use a combination of if-else statements and comparisons. Let's say we want to sort the titles in the following order: "Harry Potter", "The Great Gatsby", "A Song of Ice and Fire", and then all other titles in alphabetical order. We can define the `compareTitles()` function as follows:

```cpp
bool compareTitles(const string& title1, const string& title2) {
    if (title1 == "Harry Potter") {
        return true;
    }
    else if (title2 == "Harry Potter") {
        return false;
    }
    else if (title1 == "The Great Gatsby") {
        return true;
    }
    else if (title2 == "The Great Gatsby") {
        return false;
    }
    else if (title1 == "A Song of Ice and Fire") {
        return true;
    }
    else if (title2 == "A Song of Ice and Fire") {
        return false;
    }
    else {
        return title1 < title2;
    }
}
```

In the `compareTitles()` function above, we first handle the special cases by checking if either of the titles is equal to our special keywords ("Harry Potter", "The Great Gatsby", "A Song of Ice and Fire"). If a title matches one of these keywords, it is considered "smaller" and is placed before other titles. If neither title matches any of the keywords, we simply compare them using the `<` operator.

Now, by calling `std::sort()` with our custom comparison function, we can sort the titles according to our desired order:

```cpp
sort(titles.begin(), titles.end(), compareTitles);
```

The output of the program will be:

```
Harry Potter
The Great Gatsby
A Song of Ice and Fire
Lord of the Rings
```

In this way, you can customize the sorting logic for literals in C++ by providing a custom comparison function to `std::sort()`.

# Conclusion

Sorting is a fundamental operation in programming, and C++ provides powerful tools like the `std::sort()` function from the `<algorithm>` library to handle sorting tasks. However, there may be situations where you need to sort elements using a custom order. By defining a custom comparison function, you can easily sort literals in C++ based on your specific requirements.