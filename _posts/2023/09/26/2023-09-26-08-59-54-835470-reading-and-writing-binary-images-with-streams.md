---
layout: post
title: "Reading and writing binary images with streams"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

In this blog post, we will explore how to read and write binary images using streams in different programming languages. Streams provide a convenient way to manipulate binary data without having to load the entire image into memory at once.

Let's dive into the code examples in three popular programming languages: Python, Java, and C++.

## Reading Binary Images

### Python
```python
import numpy as np

with open("binary_image.bin", "rb") as file:
    binary_data = file.read()
    binary_image = np.frombuffer(binary_data, dtype=np.uint8)
```

### Java
```java
import java.io.DataInputStream;
import java.io.FileInputStream;
import java.io.IOException;

public class BinaryImageReader {
    public static void main(String[] args) {
        try (DataInputStream dis = new DataInputStream(new FileInputStream("binary_image.bin"))) {
            byte[] binaryData = new byte[(int)dis.length()];
            dis.readFully(binaryData);
            int[] binaryImage = new int[binaryData.length];
            
            for (int i = 0; i < binaryData.length; i++) {
                binaryImage[i] = binaryData[i] & 0xFF;
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### C++
```cpp
#include <iostream>
#include <fstream>
#include <vector>

int main() {
    std::ifstream file("binary_image.bin", std::ios::binary | std::ios::ate);
    std::streampos imageSize = file.tellg();
    file.seekg(0, std::ios::beg);

    std::vector<unsigned char> binaryData(imageSize);
    if (file.read(reinterpret_cast<char*>(binaryData.data()), imageSize)) {
        // Process binary image data
    }
    
    file.close();
}
```

## Writing Binary Images

### Python
```python
import numpy as np

binary_image = np.array([0, 1, 1, 0, 1], dtype=np.uint8)

with open("binary_image.bin", "wb") as file:
    file.write(binary_image.tobytes())
```

### Java
```java
import java.io.DataOutputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class BinaryImageWriter {
    public static void main(String[] args) {
        int[] binaryImage = {0, 1, 1, 0, 1};
        
        try (DataOutputStream dos = new DataOutputStream(new FileOutputStream("binary_image.bin"))) {
            for (int pixel : binaryImage) {
                dos.writeInt(pixel);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### C++
```cpp
#include <iostream>
#include <fstream>
#include <vector>

int main() {
    std::vector<unsigned char> binaryImage = {0, 1, 1, 0, 1};
    
    std::ofstream file("binary_image.bin", std::ios::binary);
    file.write(reinterpret_cast<char*>(binaryImage.data()), binaryImage.size());
    
    file.close();
}
```

Reading and writing binary images using streams provides an efficient and memory-optimized way to work with large image datasets. With the code examples provided in Python, Java, and C++, you can now leverage streams to perform image processing tasks on binary images effectively.

#computerVision #binaryImages