---
layout: post
title: "Reading and writing CSV files with streams"
description: " "
date: 2023-09-26
tags: [streaming]
comments: true
share: true
---

CSV (Comma-Separated Values) is a popular file format used for storing tabular data. In this blog post, we will explore how to read and write CSV files using streams in various programming languages.

### Why Use Streams?

Using streams to read and write CSV files provides several benefits:

1. Memory efficiency: Streams process data in smaller chunks, allowing you to handle large CSV files without consuming excessive memory.
2. Better performance: Streaming data from the file reduces the overall processing time as you don't have to load the whole file into memory.
3. Flexibility: Streams allow you to perform various operations on the CSV data, such as filtering, transforming, and aggregating, while reading or writing.

### Reading CSV Files with Streams

Let's start by looking at an example of reading a CSV file using streams in Python:

```python
import csv

with open('data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        # Process each row here
        print(row)
```

In this example, we use the `csv.reader` class provided by the `csv` module. The `csv.reader` takes a file object and returns an iterator that allows us to iterate over the rows in the CSV file.

Now, let's see how we can read a CSV file using streams in Java:

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class CSVReader {
    public static void main(String[] args) {
        String csvFile = "data.csv";
        String line;
        
        try (BufferedReader br = new BufferedReader(new FileReader(csvFile))) {
            while ((line = br.readLine()) != null) {
                // Process each line here
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In this Java example, we use a `BufferedReader` to read the CSV file line by line. The `readLine()` method returns each line as a string which can then be processed as needed.

### Writing CSV Files with Streams

Now let's explore how to write data to a CSV file using streams.

In Python:

```python
import csv

data = [
    ['Name', 'Age', 'Country'],
    ['John Doe', 25, 'USA'],
    ['Jane Smith', 30, 'Canada'],
    ['Alice Johnson', 35, 'UK']
]

with open('output.csv', 'w') as file:
    writer = csv.writer(file)
    writer.writerows(data)
```

Here, we use the `csv.writer` class to write data to a CSV file. The `writerows()` method allows us to write multiple rows at once.

In Java:

```java
import java.io.FileWriter;
import java.io.IOException;
import java.util.Arrays;
import java.util.List;

public class CSVWriter {
    public static void main(String[] args) {
        List<List<String>> data = Arrays.asList(
                Arrays.asList("Name", "Age", "Country"),
                Arrays.asList("John Doe", "25", "USA"),
                Arrays.asList("Jane Smith", "30", "Canada"),
                Arrays.asList("Alice Johnson", "35", "UK")
        );
        
        try (FileWriter writer = new FileWriter("output.csv")) {
            for (List<String> row : data) {
                writer.write(String.join(",", row));
                writer.write('\n');
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In this Java example, we use a `FileWriter` to write data to a CSV file. We iterate through the `data` list and write each row by joining the elements with a comma separator.

### Conclusion

Using streams to read and write CSV files offers memory efficiency, better performance, and flexibility. Whether you are working with Python or Java, the examples provided in this blog post should help you get started with processing CSV files using streams. Start streamlining your CSV file operations today!

#csv #streaming