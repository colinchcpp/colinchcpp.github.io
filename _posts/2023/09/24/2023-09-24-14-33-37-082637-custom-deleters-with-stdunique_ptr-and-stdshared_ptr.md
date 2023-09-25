---
layout: post
title: "Custom deleters with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

## `std::unique_ptr` with Custom Deleters
`std::unique_ptr` is designed to manage single ownership of dynamically allocated objects. By default, `std::unique_ptr` uses the `delete` function to deallocate memory. However, you can customize the deletion behavior by providing a lambda function, a function pointer, or a function object as the deleter.

Here is an example of using a custom deleter with `std::unique_ptr`:

```cpp
#include <iostream>
#include <memory>

struct FileDeleter {
    void operator()(FILE* file) {
        std::cout << "Closing file..." << std::endl;
        fclose(file);
    }
};

int main() {
    std::unique_ptr<FILE, FileDeleter> filePtr(fopen("myfile.txt", "w"));
    if (filePtr) {
        // File successfully opened
        // Do something with the file
    }
    // The file will be automatically closed when filePtr goes out of scope

    return 0;
}
```

In the code above, we define a custom deleter `FileDeleter` that closes the file using `fclose()`. We then use this custom deleter when declaring the `std::unique_ptr` object `filePtr`. When `filePtr` goes out of scope, the custom deleter function is automatically called, ensuring proper cleanup.

## `std::shared_ptr` with Custom Deleters
`std::shared_ptr` allows multiple smart pointers to share ownership of an object. It relies on a reference count to determine when to deallocate memory. By default, `std::shared_ptr` uses `delete` to free the memory allocated by `new`. However, you can also provide a custom deleter by passing a function or functor as the second template argument.

Here is an example of using a custom deleter with `std::shared_ptr`:

```cpp
#include <iostream>
#include <memory>

struct CustomDeleter {
    void operator()(int* ptr) {
        std::cout << "Custom deleter called..." << std::endl;
        delete ptr;
    }
};

int main() {
    std::shared_ptr<int> sharedPtr(new int(42), CustomDeleter());
    if (sharedPtr) {
        // Do something with the shared pointer
    }
    // The memory will be deallocated when the last shared_ptr goes out of scope

    return 0;
}
```

In the above code, we define a custom deleter `CustomDeleter` that uses `delete` to deallocate the memory. We pass it as the second argument to the `std::shared_ptr` constructor. When the last `std::shared_ptr` owning the resource is destroyed, the custom deleter will be called.

## Conclusion
`std::unique_ptr` and `std::shared_ptr` are powerful smart pointers that help manage dynamically allocated objects. By using custom deleters, you can specify specialized cleanup logic for these smart pointers. Whether it's closing a file or freeing memory using a custom allocation scheme, custom deleters provide flexibility in managing resources with smart pointers.

#customdeleters #smartpointers