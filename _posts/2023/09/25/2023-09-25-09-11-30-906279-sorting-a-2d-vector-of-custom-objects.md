---
layout: post
title: "Sorting a 2D vector of custom objects"
description: " "
date: 2023-09-25
tags: [programming, sorting]
comments: true
share: true
---

In certain scenarios, you might come across a situation where you need to sort a 2D vector containing custom objects in a specific order. Sorting a 2D vector can be a bit tricky compared to sorting a regular array or vector, but with the right approach, it can be easily accomplished.

Let's assume we have a 2D vector named `customObjects`, which contains objects of a custom class named `CustomObject`. Each `CustomObject` has two attributes - `name` and `score`.

```cpp
class CustomObject {
    public:
        std::string name;
        int score;
};
std::vector<std::vector<CustomObject>> customObjects;
```

Now, let's say we want to sort this 2D vector based on the `score` attribute of the `CustomObject`. To achieve this, we can use the `sort` function along with a custom comparator.

First, we need to define our custom comparator function. This function will take two `CustomObject` objects and compare their scores.

```cpp 
bool customComparator(const CustomObject& obj1, const CustomObject& obj2) {
    return obj1.score < obj2.score;
}
```

Once the comparator function is defined, we can use it with the `sort` function to sort the vector. 

```cpp
std::sort(customObjects.begin(), customObjects.end(), customComparator);
```

That's it! Now the `customObjects` 2D vector will be sorted based on the `score` attribute of the `CustomObject`. The objects with the lowest scores will be at the beginning of the vector, while the objects with the highest scores will be at the end.

## Conclusion

In this article, we learned how to sort a 2D vector of custom objects in C++. By defining a custom comparator function and using it with the `sort` function, we can easily sort the vector based on the desired attribute of the objects. This technique can be useful in various scenarios where sorting a 2D vector is required.

#programming #cpp #sorting