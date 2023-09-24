---
layout: post
title: "Creating arrays with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

Using `std::unique_ptr` with Arrays:

To create an array using `std::unique_ptr`, you can specify a custom deleter that uses `delete[]` to free the memory allocated for the array. Here's an example of how to create a dynamic array with `std::unique_ptr`:

```cpp
#include <memory>

int main() {
  int size = 10;
  std::unique_ptr<int[]> uniqueArray(new int[size]);
  
  // Access and modify elements of the array
  for (int i = 0; i < size; ++i) {
    uniqueArray[i] = i;
  }
  
  return 0;
}
```

In the above code, we create a `std::unique_ptr` named `uniqueArray` of type `int[]`, indicating that it points to an array of integers. We allocate memory for the array using `new int[size]`.

Using `std::shared_ptr` with Arrays:

Unlike `std::unique_ptr`, `std::shared_ptr` does not provide a default deleter for arrays. To use `std::shared_ptr` with arrays, we need to provide a custom deleter using a lambda function or a deleter function object. Here's an example:

```cpp
#include <memory>

struct ArrayDeleter {
  template <typename T>
  void operator()(T* arr) {
    delete[] arr;
  }
};

int main() {
  int size = 10;
  std::shared_ptr<int> sharedArray(new int[size], ArrayDeleter());
  
  // Access and modify elements of the array
  for (int i = 0; i < size; ++i) {
    sharedArray.get()[i] = i;
  }
  
  return 0;
}
```

In the above code, we define a custom deleter `ArrayDeleter` that uses `delete[]` to free the memory allocated for the array. We then pass an instance of this deleter as the second argument to the `std::shared_ptr` constructor.

Using `std::unique_ptr` and `std::shared_ptr` for arrays provides several advantages, such as automatic resource management, preventing memory leaks, and reducing the risk of dangling pointers. However, keep in mind that the size of the array must be known at the time of allocation and cannot be changed dynamically. It's also important to choose the appropriate smart pointer type based on your requirements, considering factors like ownership semantics and performance.

#C++ #SmartPointers