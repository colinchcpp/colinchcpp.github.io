---
layout: post
title: "Sharing objects across translation units with `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [ifndef, define]
comments: true
share: true
---

When it comes to sharing objects across translation units in C++, one popular approach is to use smart pointers. One of the most commonly used smart pointers in C++ is `std::shared_ptr`, which provides automatic memory management through reference counting.

## What is `std::shared_ptr`?

`std::shared_ptr` is a smart pointer provided by the C++ Standard Library that allows multiple pointers to share ownership of an object. It keeps track of the number of shared pointers pointing to the object, and when the last shared pointer goes out of scope, the object is automatically deleted.

## Sharing objects across translation units

To share an object across multiple translation units using `std::shared_ptr`, you need to follow these steps:

1. Create a class or object that needs to be shared.
2. Use `std::shared_ptr` to wrap the object.
3. Include the header file that contains the declaration of the shared object in all translation units that need to use it.
4. Link all translation units together during the compilation process.

Let's take a look at an example:

```cpp
// shared_object.h
#ifndef SHARED_OBJECT_H
#define SHARED_OBJECT_H

#include <memory>

class SharedObject {
public:
    void doSomething() {
        // Implementation goes here
    }
};

#endif
```

```cpp
// main.cpp
#include "shared_object.h"

int main() {
    std::shared_ptr<SharedObject> sharedObject = std::make_shared<SharedObject>();

    sharedObject->doSomething();

    return 0;
}
```

```cpp
// other.cpp
#include "shared_object.h"

void someFunction() {
    std::shared_ptr<SharedObject> sharedObject = std::make_shared<SharedObject>();

    sharedObject->doSomething();
}
```

In this example, we have a shared object called `SharedObject`. It is wrapped inside a `std::shared_ptr` in both `main.cpp` and `other.cpp`. Both translation units include the `shared_object.h` header file which contains the declaration of `SharedObject`. These translation units can use the shared object and call its member functions as needed.

During the compilation process, all translation units are compiled separately, and then linked together. This allows the shared object to be accessed and used across multiple translation units.

## Conclusion

Using `std::shared_ptr` is a powerful way to share objects across translation units in C++. By following the steps mentioned above, you can easily share objects and ensure their proper memory management. Just remember to include the necessary header files and link the translation units together during compilation.

#C++ #SmartPointers