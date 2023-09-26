---
layout: post
title: "Reading and writing integers with streams"
description: " "
date: 2023-09-26
tags: [Java, Streams]
comments: true
share: true
---

Reading Integers from a Stream:

To read integers from a stream in Java, we can use the `Scanner` class. Here's an example:

```java
import java.util.Scanner;

public class ReadIntegers {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter a number: ");
        int number = scanner.nextInt();

        System.out.println("You entered: " + number);

        scanner.close();
    }
}
```

In this example, we create an instance of the `Scanner` class, passing `System.in` as the argument to read input from the standard input stream. We then use the `nextInt()` method to read an integer from the stream. Finally, we print the entered number to the console.

Writing Integers to a Stream:

To write integers to a stream in Java, we can use the `PrintStream` class. Here's an example:

```java
import java.io.FileOutputStream;
import java.io.PrintStream;

public class WriteIntegers {
    public static void main(String[] args) {
        try {
            FileOutputStream fileOutputStream = new FileOutputStream("output.txt");
            PrintStream printStream = new PrintStream(fileOutputStream);

            printStream.println(10);
            printStream.println(20);
            printStream.println(30);

            printStream.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

In this example, we create an instance of `FileOutputStream` to write to a file named "output.txt". We then create a `PrintStream` instance, passing `fileOutputStream` as the argument. We use the `println()` method to write integers to the stream, and finally, we close the stream.

Advantages of Using Streams:

Using streams for reading and writing integers has several advantages. First, streams provide a simple and intuitive way to handle input and output operations. The code becomes cleaner and more readable.

Secondly, streams handle different types of data efficiently. For example, you can read and write integers, strings, or even complex objects using the same stream interface. This flexibility simplifies code maintenance and reduces duplication.

In addition, streams provide error handling mechanisms such as exception handling. If any error occurs during input or output operations, appropriate exceptions can be thrown and caught.

In conclusion, using streams to read and write integers provides a clean, efficient, and flexible approach. It simplifies code and provides error handling mechanisms. By leveraging the power of streams, developers can create robust and maintainable programs.

#Java #Streams