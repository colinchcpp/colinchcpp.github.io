---
layout: post
title: "Constructors for Builder Patterns in C++"
description: " "
date: 2023-09-23
tags: [BuilderPattern]
comments: true
share: true
---

The Builder pattern is a creational design pattern that aims to simplify the creation of complex objects by separating the construction process from the object's representation. One way to implement the Builder pattern in C++ is by using constructors in the builder class. In this blog post, we'll explore how to implement constructors for the Builder pattern in C++

## Overview of the Builder Pattern

The Builder pattern involves three main components:

1. **Product**: Represents the complex object that we want to create.
2. **Builder**: Abstract class or interface that defines the construction process and provides methods for setting the properties of the product.
3. **Concrete Builder**: Implements the builder interface and provides specific implementations for constructing different parts of the product.
4. **Director**: Controls the construction process and uses the builder to create the final product.

The goal of the Builder pattern is to provide a flexible and structured way to construct complex objects step by step, by allowing the client to specify only the required properties.

## Constructor-based Implementation

To implement the Builder pattern using constructors in C++, we can define a builder class that takes the necessary parameters in its constructor. The builder class can then have additional methods for setting optional properties. Here's an example:

```cpp
class ProductBuilder {
private:
    std::string prop1;
    int prop2;
    // Add more properties as needed

public:
    ProductBuilder(const std::string& prop1, int prop2) : prop1(prop1), prop2(prop2) {}

    ProductBuilder& setProp1(const std::string& value) {
        prop1 = value;
        return *this;
    }

    ProductBuilder& setProp2(int value) {
        prop2 = value;
        return *this;
    }

    // Add more setter methods as needed

    Product build() {
        return Product(prop1, prop2);
    }
};
```

In the above code, the `ProductBuilder` class has a constructor that takes the mandatory properties `prop1` (a string) and `prop2` (an integer). To set the optional properties, setter methods are provided, which return a reference to the builder itself to enable method chaining.

The `build()` method creates and returns the final `Product` object using the properties set in the builder.

## Creating the Product

To create the `Product` object using the builder, we can use the following code:

```cpp
ProductBuilder builder("value1", 42);
Product product = builder.setProp1("new value").setProp2(99).build();
```

In the code above, we first create a `ProductBuilder` object with the mandatory properties. Then, we can set the optional properties using the setter methods and finally call the `build()` method to obtain the `Product` object.

## Conclusion

By using constructors in the builder class, we can implement the Builder pattern in C++ and create complex objects in a structured and flexible manner. This allows us to define the construction process step by step and specify only the required properties. This pattern promotes loose coupling and enhances code readability and maintainability.

#C++ #BuilderPattern