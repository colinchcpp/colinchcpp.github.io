---
layout: post
title: "Initialization of structs using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: [cplusplus, structs]
comments: true
share: true
---

In C++, structs are a composite data type used to group related variables together. Prior to C++11, initializing struct objects involved using constructor functions or initializing each member individually. However, with the introduction of uniform initialization in C++11, initializing structs has become more concise and intuitive.

Uniform initialization allows the initialization of structs using brace-initialization syntax (`{}`), making the code more readable and consistent across different types of objects. Let's explore how it works:

## 1. Default Initialization

With uniform initialization, you can initialize a struct using the default constructor by simply using empty braces `{}`. This initializes each member of the struct with their default values.

```cpp
struct Person {
    std::string name;
    int age;
};

int main() {
    Person person{}; // Default initializes person struct

    // Accessing members of the struct
    person.name = "John Doe";
    person.age = 25;

    return 0;
}
```

In the above code, we initialize a person struct using default initialization and then assign values to its members.

## 2. Value Initialization

Uniform initialization also allows for value initialization, where each member of the struct is initialized with explicit values. This eliminates the need for constructors or explicit member initialization.

```cpp
struct Point {
    int x;
    int y;
};

int main() {
    Point point{1, 2}; // Value initializes point struct

    // Accessing members of the struct
    std::cout << "x: " << point.x << ", y: " << point.y << std::endl;

    return 0;
}
```

In the above code, we initialize a point struct using value initialization with explicit x and y values.

## 3. Aggregate Initialization

Structs that meet certain conditions can utilize aggregate initialization, where braces are used to initialize each member of the struct in order.

```cpp
struct Color {
    int red;
    int green;
    int blue;
};

int main() {
    Color color{255, 128, 64}; // Aggregate initializes color struct

    // Accessing members of the struct
    std::cout << "red: " << color.red << ", green: " << color.green << ", blue: " << color.blue << std::endl;

    return 0;
}
```

In the above code, we initialize a color struct using aggregate initialization, with explicit values for red, green, and blue.

## Conclusion

With the introduction of uniform initialization in C++, initializing structs has become more convenient, readable, and consistent. You can now easily initialize structs using default initialization, value initialization, or aggregate initialization, based on your needs. This feature has made initialization of structs more concise and efficient in modern C++ code.

To learn more about uniform initialization in C++, refer to the [C++ documentation](https://en.cppreference.com/w/cpp/language/aggregate_initialization) and explore other features of C++ syntax. #cplusplus #structs