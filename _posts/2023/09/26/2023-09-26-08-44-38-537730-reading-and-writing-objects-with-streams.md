---
layout: post
title: "Reading and writing objects with streams"
description: " "
date: 2023-09-26
tags: [Java, ObjectSerialization]
comments: true
share: true
---

In object-oriented programming, it is common to work with objects that need to be saved to and retrieved from a persistent storage medium, such as a file or a database. One of the ways to achieve this is by using streams to read and write objects.

Streams provide a convenient way to transfer data in a sequential manner. In Java, there are two types of streams: input streams and output streams. Input streams allow you to read data from a source, while output streams allow you to write data to a destination.

### Object Serialization

Java provides a mechanism called **object serialization** that allows objects to be converted into a stream of bytes and saved to a file or sent over a network. The reverse process of converting the serialized object back into its original form is called **deserialization**.

To make an object serializable, it needs to implement the `Serializable` interface. This interface acts as a marker indicating that the object can be serialized. Once an object is serializable, it can be written to an output stream and later read back from an input stream.

### Writing Objects to a File

To write an object to a file, we first need to create an output stream. In Java, the `FileOutputStream` class provides a way to write bytes to a file. We can use this class to create an output stream and then wrap it with an `ObjectOutputStream` to enable writing objects.

Here's an example that demonstrates how to write a serialized object to a file using output streams:

```java
FileOutputStream fileOutputStream = new FileOutputStream("object.ser");
ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
objectOutputStream.writeObject(object); // object is the object to be serialized
objectOutputStream.close();
```

### Reading Objects from a File

To read an object from a file, we need to create an input stream. In Java, the `FileInputStream` class allows us to read bytes from a file. Like before, we can wrap this class with an `ObjectInputStream` to enable reading objects.

Here's an example that shows how to read a serialized object from a file using input streams:

```java
FileInputStream fileInputStream = new FileInputStream("object.ser");
ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
Object object = objectInputStream.readObject();
objectInputStream.close();
```

### Conclusion

Using streams to read and write objects provides a flexible and efficient way to handle persistence in an object-oriented system. By serializing objects and writing them to a stream, we can easily save them to a file or send them over a network. Conversely, we can deserialize objects from a stream to reconstruct them and continue working with them.

By understanding how to use streams effectively, you can leverage this feature in your Java applications to store and retrieve objects seamlessly.

**#Java #ObjectSerialization**