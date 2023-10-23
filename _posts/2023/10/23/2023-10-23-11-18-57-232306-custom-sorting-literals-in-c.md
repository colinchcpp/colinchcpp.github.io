---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting elements is a common task in many programming applications. C++ provides a powerful sorting function, `std::sort`, which can sort elements based on the default ordering provided by the `<` (less than) operator. However, there are cases when we may need to sort elements based on a custom ordering that is not supported by the default comparison operator. In such cases, we can specify our own custom sorting literals.

## Defining Custom Sorting Literals

To define custom sorting literals, we need to provide a comparison function or functor that defines the desired ordering of the elements. This can be achieved in a few different ways.

### Function-based approach

Here is an example of a custom sorting literal using a comparison function:

```cpp
bool compareByLength(const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
}

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};
    
    std::sort(words.begin(), words.end(), compareByLength);
    
    for (const auto& word : words) {
        std::cout << word << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

In this example, we define a comparison function `compareByLength` that compares the length of two strings. We then pass this function as the third argument to `std::sort` to sort the vector `words` based on the length of the strings. The output will be: `date apple banana cherry`.

### Functor-based approach

Alternatively, we can define a functor to provide the custom sorting literal. Here's an example:

```cpp
struct CompareByLength {
    bool operator()(const std::string& str1, const std::string& str2) {
        return str1.length() < str2.length();
    }
};

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};
    
    std::sort(words.begin(), words.end(), CompareByLength());
    
    for (const auto& word : words) {
        std::cout << word << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

In this case, we define a functor `CompareByLength` which overloads the `operator()` to perform the comparison. We then create an instance of this functor and pass it as the third argument to `std::sort`.

## Conclusion

Custom sorting literals in C++ allow us to define our own ordering criteria based on specific requirements. Whether using a comparison function or a functor, we can utilize custom sorting literals to sort elements in a way that is tailored to our needs.

By utilizing custom sorting literals, we can sort elements based on any desired property or criteria, providing us with more flexibility and control over the sorting process.

##### References:
- [C++ Reference - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)