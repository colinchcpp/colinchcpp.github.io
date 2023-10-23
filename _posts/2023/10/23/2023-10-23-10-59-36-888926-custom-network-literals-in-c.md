---
layout: post
title: "Custom network literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

In C++, literals are used to represent values of various types directly in the source code. For example, `42` is an integer literal, `"hello"` is a string literal, and `3.14` is a floating-point literal. 

C++ provides the ability to create custom literals and use them to represent your own types. One interesting use case is creating custom network literals to represent IP addresses or URL literals.

## Defining a Custom Literal Operator

To define a custom network literal, we can create a user-defined literal operator function. This function will be called when the literal is encountered in the code. 

Here's an example of how to define a custom literal operator for a network address:

```cpp
#include <iostream>
#include <string>

struct NetworkAddress {
    std::string address;
    int port;
};

NetworkAddress operator"" _net(const char* addr, std::size_t size) {
    std::string address(addr, size);
    // Parse the address and extract the port number
    // Here, we assume that the address is in the format "address:port"
    size_t pos = address.find(':');
    int port = std::stoi(address.substr(pos + 1));

    return NetworkAddress{address.substr(0, pos), port};
}
```

In the above code, we define a `NetworkAddress` structure and a literal operator function `operator"" _net`. The operator function takes a `const char*` and `std::size_t` as parameters representing the string literal and its size, respectively. 

Inside the operator function, we parse the string literal to extract the address and port number. We assume that the address is in the format "address:port". 

## Using the Custom Network Literal

Once the custom literal operator is defined, we can use it to create instances of our custom type. Here's an example:

```cpp
void connect(const NetworkAddress& address) {
    std::cout << "Connecting to " << address.address << " on port " << address.port << std::endl;
}

int main() {
    auto serverAddress = "127.0.0.1:8080"_net;
    connect(serverAddress);

    return 0;
}
```

In the `main` function, we create a `serverAddress` variable using the custom network literal `_net`. The literal value "127.0.0.1:8080" is parsed by the custom operator function to create the `NetworkAddress` object.

We can then pass the `serverAddress` to the `connect` function and perform the desired networking tasks.

## Conclusion

Custom network literals allow us to conveniently represent network addresses or URLs directly in the source code and parse them into structured objects. This can make networking-related code more readable and expressive.

Keep in mind that custom literals should be used judiciously and follow a clear convention to avoid confusion and maintain readability.

#References
- [User-defined literals (C++ reference)](https://en.cppreference.com/w/cpp/language/user_literal)