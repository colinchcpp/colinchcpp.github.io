---
layout: post
title: "Removing duplicates from a vector"
description: " "
date: 2023-09-25
tags: [programming, vectors]
comments: true
share: true
---

## 1. Python

In Python, you can easily remove duplicates from a vector using the `set` data structure. Here's an example:

```python
vector = [1, 2, 3, 3, 4, 5, 5]

unique_vector = list(set(vector))

print(unique_vector)
```

Output:
```
[1, 2, 3, 4, 5]
```

In the code snippet above, we convert the `vector` list to a set using `set(vector)`, which automatically removes any duplicate elements. Then, we convert it back to a list using `list()` to retain the original order.

## 2. Java

In Java, you can remove duplicates from a vector by creating a `HashSet`, which is similar to a Python set, and then converting it back to a vector. Here's an example:

```java
import java.util.*;

public class DuplicateRemoval {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>(Arrays.asList(1, 2, 3, 3, 4, 5, 5));

        HashSet<Integer> set = new HashSet<>(vector);
        vector.clear();
        vector.addAll(set);

        System.out.println(vector);
    }
}
```

Output:
```
[1, 2, 3, 4, 5]
```

In the above code snippet, we create a `HashSet<Integer>` using the `vector`, which automatically removes duplicates. Then, we clear the original vector and add all elements from the `HashSet` back into the vector.

## Conclusion

Removing duplicates from a vector is a common task in programming. By utilizing built-in data structures like sets or hash sets, we can easily accomplish this task. These approaches ensure that the vector only contains unique elements, helping to avoid any errors or unnecessary operations.

#programming #vectors #duplicate-removal