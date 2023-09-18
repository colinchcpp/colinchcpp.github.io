---
layout: post
title: "Serializing and deserializing collections of C++ objects with variable sizes"
description: " "
date: 2023-09-19
tags: [CPlusPlus, Serialization]
comments: true
share: true
---

Serialization is the process of converting complex objects into a format that can be stored or transmitted. Deserialization is the reverse process of converting the serialized data back into objects. In C++, we can use serialization to store collections of objects with variable sizes, making it easier to persist and transport data.

## Serializing Objects

To serialize a collection of objects with variable sizes, we need to define a serialization method for each object. The serialization method should convert the object's data into a serialized format, such as a binary or text representation.

Let's take an example of a `Person` class with `name` and `age` attributes. To serialize the `Person` objects, we can define a serialization method as follows:

```cpp
class Person {
public:
    std::string name;
    int age;

    // Serialize the Person object to a string
    std::string serialize() const {
        std::ostringstream oss;
        oss << name << "," << age;
        return oss.str();
    }
};
```

In the `serialize()` method, we use an `ostringstream` to convert the `name` and `age` into a string format, separated by a comma.

## Serializing Collections

Now that we have the serialization method for individual objects, we can proceed to serialize collections of objects.

Let's say we have a vector of `Person` objects:

```cpp
std::vector<Person> people = { {"Alice", 25}, {"Bob", 30}, {"Charlie", 35} };
```

To serialize this vector, we can loop over each object and call the `serialize()` method. We can then store the serialized strings in another container, such as a vector or a file.

```cpp
std::vector<std::string> serializedPeople;

for (const auto& person : people) {
    serializedPeople.push_back(person.serialize());
}
```

The `serializedPeople` vector now contains the serialized strings of each `Person` object.

## Deserializing Objects

Deserialization is the process of converting the serialized data back into objects. To deserialize the serialized strings of `Person` objects, we need to define a deserialization method.

```cpp
// Deserialize a string into a Person object
Person deserialize(const std::string& serializedString) {
    std::istringstream iss(serializedString);
    std::string name;
    int age;

    std::getline(iss, name, ',');
    iss >> age;

    return { name, age };
}
```

In the `deserialize()` method, we use an `istringstream` to split the serialized string into `name` and `age` parts. By using `getline()` with the ',' delimiter, we can extract the `name`, and then use `>>` to extract the `age`.

## Deserializing Collections

To deserialize a collection of serialized objects, we can iterate over the serialized strings and apply the `deserialize()` method to each string.

```cpp
std::vector<Person> deserializedPeople;

for (const auto& serializedPerson : serializedPeople) {
    deserializedPeople.push_back(deserialize(serializedPerson));
}
```

Now, the `deserializedPeople` vector contains the `Person` objects that were deserialized from the serialized strings.

## Conclusion

Serializing and deserializing collections of C++ objects with variable sizes allows us to store and transmit complex data structures. By defining serialization and deserialization methods for individual objects, we can convert them into a format that can be easily stored or transported. This enables us to effectively manage data in C++ applications. #CPlusPlus #Serialization