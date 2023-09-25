---
layout: post
title: "Serializing and deserializing C++ objects with non-public member variables"
description: " "
date: 2023-09-19
tags: [serialization]
comments: true
share: true
---
title: Serializing and Deserializing C++ Objects with Non-Public Member Variables
tags: #C++ #serialization
---

Serializing and deserializing objects is a common requirement in many applications, allowing data to be stored or transmitted in a format that can be easily reconstructed. This process becomes slightly more complex when dealing with C++ objects that have non-public member variables. In this article, we will explore how to properly serialize and deserialize such objects.

## Serialization

Serialization is the process of converting an object instance into a data format that can be persisted or transmitted. In C++, there are several libraries available for serialization, such as Boost.Serialization and Protocol Buffers. For this example, we will use the Boost.Serialization library.

To serialize a C++ object with non-public member variables, we need to provide a mechanism to access those members. One way to achieve this is by declaring serialization functions `save` and `load` as friends of the class.

```cpp
#include <boost/archive/text_oarchive.hpp>
#include <boost/archive/text_iarchive.hpp>
#include <fstream>

class MyClass {
private:
    int privateVariable;

    friend class boost::serialization::access;
    template<class Archive>
    void serialize(Archive& ar, const unsigned int version) {
        ar & privateVariable;
    }
public:
    // ...
};
```

In the code snippet above, we declare the serialization functions `save` and `load` as friends of the `MyClass` class. This allows them to access the private member `privateVariable`. We then provide the implementation of the `serialize` function, specifying how the object should be serialized.

To serialize an instance of `MyClass` into a text file, we can use the `boost::archive::text_oarchive` class:

```cpp
void serializeObject(const MyClass& obj, const std::string& filename) {
    std::ofstream ofs(filename);
    boost::archive::text_oarchive oa(ofs);
    oa << obj;
}
```

The `serializeObject` function takes an instance of `MyClass` and a filename, opens an output stream to the file, and creates a `boost::archive::text_oarchive` object to write the serialized data.

## Deserialization

Deserialization is the process of reconstructing an object from a serialized form. To deserialize a C++ object with non-public member variables, we follow a similar approach as serialization.

First, declare the `load` function as a friend of the class and implement the `serialize` function:

```cpp
class MyClass {
private:
    int privateVariable;

    friend class boost::serialization::access;
    template<class Archive>
    void serialize(Archive& ar, const unsigned int version) {
        ar & privateVariable;
    }
public:
    // ...

    friend void loadObject(MyClass& obj, const std::string& filename);
};
```

Here, we declare the `load` function as a friend of `MyClass` so it can access the private member variables. We also declare the `loadObject` function which will be responsible for deserialization.

To deserialize an object from a text file, we use the `boost::archive::text_iarchive` class:

```cpp
void loadObject(MyClass& obj, const std::string& filename) {
    std::ifstream ifs(filename);
    boost::archive::text_iarchive ia(ifs);
    ia >> obj;
}
```

The `loadObject` function takes an instance of `MyClass` and a filename, opens an input stream from the file, and creates a `boost::archive::text_iarchive` object to read the serialized data. It then reads the data into the provided object.

## Conclusion

Serialization and deserialization of C++ objects with non-public member variables can be achieved by declaring serialization functions as friends of the classes and using serialization libraries like Boost.Serialization. By doing so, we can properly access and store the private members during serialization, and reconstruct the object during deserialization. This allows for effective persistence and transmission of data within C++ applications.