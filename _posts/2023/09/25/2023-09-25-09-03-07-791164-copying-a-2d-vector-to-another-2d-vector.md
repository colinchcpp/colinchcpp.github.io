---
layout: post
title: "Copying a 2D vector to another 2D vector"
description: " "
date: 2023-09-25
tags: [python, vector]
comments: true
share: true
---

Let's assume we have two 2D vectors, `vector1` and `vector2`, both of the same size. Our goal is to copy the elements from `vector1` into `vector2` so that both vectors contain the same values.

Here's a simple and efficient way to achieve this:

```python
vector1 = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
vector2 = [[] for _ in range(len(vector1))]

for i in range(len(vector1)):
    vector2[i] = vector1[i][:]
```

In the above code snippet, we first initialize an empty `vector2` by using a list comprehension. The size of `vector2` is the same as `vector1`, and each sub-list is initially empty.

Next, we iterate over the indices of `vector1` using a `for` loop. Inside the loop, we use the slice notation `vector1[i][:]` to create a copy of the elements in `vector1[i]`. This ensures that modifying `vector2` later won't affect `vector1`.

After running this code, `vector2` will contain the same elements as `vector1`. It's important to note that this method works correctly for any 2D vector, irrespective of its size or the values stored within it.

Using this technique, you can easily copy the contents of one 2D vector to another in Python.

#python #vector