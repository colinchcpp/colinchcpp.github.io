---
layout: post
title: "Initializing std::array of std::stringstreams using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

To initialize a `std::array` of `std::stringstream` objects, you can use the following syntax:

```cpp
#include <array>
#include <sstream>

int main() {
    std::array<std::stringstream, 3> streams{
        std::stringstream{},
        std::stringstream{},
        std::stringstream{}
    };

    // Use the streams...
    streams[0] << "Hello ";
    streams[1] << "world!";
    streams[2] << " How are you?";

    // Print the contents of the streams
    for (const auto& stream : streams) {
        std::cout << stream.str() << "\n";
    }

    return 0;
}
```

In the above example, we have created a `std::array` of `std::stringstream` objects with size 3. Each element is default-initialized with an empty stream. You can access and use individual streams by indexing into the array.

In this case, we have used the streams to write different strings using the `<<` operator. Finally, we print the contents of each stream using the `str()` function, which returns the string representation of the stream's content.

Output:
```
Hello 
world!
 How are you?
```

Initializing `std::array` of `std::stringstreams` using uniform initialization allows you to easily manage a collection of string streams without explicitly invoking constructors for each stream. It provides a more concise and readable way to initialize multiple objects.