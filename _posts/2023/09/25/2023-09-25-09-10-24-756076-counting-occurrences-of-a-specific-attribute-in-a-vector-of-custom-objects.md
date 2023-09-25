---
layout: post
title: "Counting occurrences of a specific attribute in a vector of custom objects"
description: " "
date: 2023-09-25
tags: [programming, python]
comments: true
share: true
---

## The Problem

Let's say we have a vector `my_vector` containing custom objects, and each object has an attribute called `attribute_name`. Our goal is to count the number of times a specific value appears in this attribute.

## The Solution

To solve this problem, we can iterate over the vector and check the value of the attribute for each object. We will use a dictionary to store the count of each value encountered.

Here's an example code snippet that demonstrates this approach:

```python
# Define the custom object
class MyObject:
    def __init__(self, attribute_name):
        self.attribute_name = attribute_name

# Create the vector of custom objects
my_vector = [
    MyObject("value1"),
    MyObject("value2"),
    MyObject("value1"),
    MyObject("value3"),
    MyObject("value2")
]

# Initialize an empty dictionary
count_dict = {}

# Iterate over the vector
for obj in my_vector:
    # Get the attribute value
    attribute_value = obj.attribute_name
    
    # Update the count in the dictionary
    count_dict[attribute_value] = count_dict.get(attribute_value, 0) + 1

# Output the counts
for attribute_value, count in count_dict.items():
    print(f"Value: {attribute_value}, Count: {count}")
```

In this example, we first define the `MyObject` class with an `attribute_name` attribute. We then create a `my_vector` list containing instances of `MyObject`, each with a different value for `attribute_name`.

Next, we initialize an empty dictionary `count_dict` to store the counts. We iterate over the `my_vector` list, retrieving the attribute value for each object. Using the `get` method of the dictionary, we retrieve the current count for the attribute value. If the value is not present in the dictionary, we default to `0`. We increment the count by `1` and update the dictionary accordingly.

Finally, we loop over the dictionary and output the attribute values along with their respective counts.

## Conclusion

By using a dictionary to store the count of attribute values, we can easily count the occurrences of a specific attribute in a vector of custom objects. This approach can be helpful in various scenarios where data analysis or processing is involved. Remember to adapt the code to your specific needs and data structures.

#programming #python