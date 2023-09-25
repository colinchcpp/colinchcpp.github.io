---
layout: post
title: "Implementing custom iterators for vectors"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

In this blog post, we will explore how to implement custom iterators for vectors in C++. Iterators are an essential part of the Standard Template Library (STL) and allow us to iterate over containers like vectors in a flexible and convenient way. By implementing custom iterators, we can add additional functionality to our vectors and make them even more powerful.

Before we dive into the implementation, let's briefly review what iterators are. Iterators provide a way to access and manipulate elements within a container. They act as pointers to elements in the container and allow us to iterate over its elements in a sequential manner. The STL provides different types of iterators, such as `begin()` and `end()`, to define the range of elements we want to iterate over.

## Custom Iterator Implementation

To implement custom iterators for vectors, we need to define a class and specify the necessary operations for it to behave like an iterator. Let's name our class `VectorIterator`.

First, we need to include the necessary headers for vector and iterator:

```cpp
#include <vector>
#include <iterator>
```

Now let's define our `VectorIterator` class:

```cpp
template<typename T>
class VectorIterator {
public:
    using iterator_category = std::forward_iterator_tag;
    using value_type = T;
    using difference_type = std::ptrdiff_t;
    using pointer = T*;
    using reference = T&;
    
    explicit VectorIterator(pointer ptr) : ptr_(ptr) {}
    
    reference operator*() const {
        return *ptr_;
    }
    
    pointer operator->() const {
        return ptr_;
    }
    
    VectorIterator& operator++() {
        ++ptr_;
        return *this;
    }
    
    VectorIterator operator++(int) {
        VectorIterator temp = *this;
        ++(*this);
        return temp;
    }
    
    friend bool operator==(const VectorIterator& lhs, const VectorIterator& rhs) {
        return lhs.ptr_ == rhs.ptr_;
    }
    
    friend bool operator!=(const VectorIterator& lhs, const VectorIterator& rhs) {
        return !(lhs == rhs);
    }
    
private:
    pointer ptr_;
};
```

Here's a breakdown of the important parts of the implementation:

- We define the necessary type aliases required by the iterator interface.
- The constructor takes a pointer to the vector's element and initializes the `ptr_` member variable.
- The `operator*` and `operator->` provide access to the element the iterator is currently pointing to.
- The pre-increment (`operator++`) and post-increment (`operator++(int)`) operators move the iterator to the next element.
- The `operator==` and `operator!=` are used to compare two iterators for equality.

## Using Custom Iterators

To use our custom iterators, we need to make a few modifications to our vector class. In the vector class definition, we should add the following typedefs:

```cpp
using iterator = VectorIterator<T>;
using const_iterator = VectorIterator<const T>;
```

By providing these typedefs, we allow users of our vector class to access the custom iterators using `vector_type::iterator` and `vector_type::const_iterator`, respectively.

Once these modifications are made, we can use our custom iterators to iterate over elements in the vector:

```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5};
for (auto it = myVector.begin(); it != myVector.end(); ++it) {
    // Do something with *it
}
```

## Conclusion

Implementing custom iterators for vectors allows us to extend the functionality of the STL and customize the way we iterate over vector elements. By defining our own iterator class and providing the necessary operations, we can make our code more expressive and efficient. Custom iterators are a powerful tool in C++ that can greatly enhance our programming experience.