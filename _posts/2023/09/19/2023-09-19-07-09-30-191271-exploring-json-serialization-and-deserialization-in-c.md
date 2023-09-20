---
layout: post
title: "Exploring JSON serialization and deserialization in C++"
description: " "
date: 2023-09-19
tags: [JSONSerialization]
comments: true
share: true
---

JSON (JavaScript Object Notation) is a popular data interchange format that is widely used in web development and API communication. In C++, there are several libraries available that provide the functionality to serialize (convert objects to JSON) and deserialize (convert JSON back to objects). In this blog post, we will explore some of the commonly used libraries and how to perform JSON serialization and deserialization in C++.

## 1. cJSON

[cJSON](https://github.com/DaveGamble/cJSON) is a lightweight, portable JSON library that provides a simple API for manipulating JSON data in C and C++ programs. It is widely used and has an active community. To use cJSON for JSON serialization and deserialization, you need to download the library from the GitHub repository and include the `cJSON.h` header file in your C++ program.

### JSON Serialization with cJSON

To serialize an object to JSON using cJSON, you need to create a cJSON object and add properties to it using the `cJSON_Add*` functions. Here's an example of serializing an object to JSON:

```cpp
#include "cJSON.h"

int main() {
   // Create cJSON root object
   cJSON* root = cJSON_CreateObject();

   // Add properties to the root object
   cJSON_AddStringToObject(root, "name", "John Doe");
   cJSON_AddNumberToObject(root, "age", 30);
   cJSON_AddBoolToObject(root, "isStudent", true);

   // Serialize the cJSON object to JSON
   char* jsonString = cJSON_Print(root);

   // Output the JSON string
   printf("%s\n", jsonString);

   // Free resources
   cJSON_Delete(root);
   free(jsonString);

   return 0;
}
```

### JSON Deserialization with cJSON

To deserialize JSON back to an object using cJSON, you can parse the JSON string and extract properties from the cJSON object. Here's an example of deserializing JSON:

```cpp
#include "cJSON.h"

int main() {
   // JSON string to deserialize
   const char* jsonString = "{\"name\":\"John Doe\",\"age\":30,\"isStudent\":true}";

   // Parse the JSON string
   cJSON* root = cJSON_Parse(jsonString);

   // Extract properties from the cJSON object
   const char* name = cJSON_GetObjectItem(root, "name")->valuestring;
   int age = cJSON_GetObjectItem(root, "age")->valueint;
   bool isStudent = cJSON_GetObjectItem(root, "isStudent")->valueint;

   // Output the extracted properties
   printf("Name: %s\n", name);
   printf("Age: %d\n", age);
   printf("Is Student: %s\n", isStudent ? "true" : "false");

   // Free resources
   cJSON_Delete(root);

   return 0;
}
```

## 2. RapidJSON

[RapidJSON](https://rapidjson.org/) is another popular JSON library in C++ that provides high-performance JSON manipulation capabilities. It is feature-rich, easy to use, and has good documentation. To use RapidJSON, you can download the library from the official website or include it as a dependency in your project.

### JSON Serialization with RapidJSON

To serialize an object to JSON using RapidJSON, you need to create a `rapidjson::Document` object, add properties to it using the `rapidjson::Value` class, and then convert it to a JSON string. Here's an example:

```cpp
#include "rapidjson/document.h"
#include "rapidjson/writer.h"
#include "rapidjson/stringbuffer.h"

int main() {
   // Create a rapidjson document
   rapidjson::Document document;
   document.SetObject();

   // Add properties to the document
   document.AddMember("name", "John Doe", document.GetAllocator());
   document.AddMember("age", 30, document.GetAllocator());
   document.AddMember("isStudent", true, document.GetAllocator());

   // Convert document to JSON string
   rapidjson::StringBuffer buffer;
   rapidjson::Writer<rapidjson::StringBuffer> writer(buffer);
   document.Accept(writer);

   // Output the JSON string
   printf("%s\n", buffer.GetString());

   return 0;
}
```

### JSON Deserialization with RapidJSON

To deserialize JSON using RapidJSON, you can parse the JSON string and access the properties using the `rapidjson::Value` class. Here's an example:

```cpp
#include "rapidjson/document.h"

int main() {
   // JSON string to deserialize
   const char* jsonString = "{\"name\":\"John Doe\",\"age\":30,\"isStudent\":true}";

   // Parse the JSON string
   rapidjson::Document document;
   document.Parse(jsonString);

   // Extract properties from the document
   const char* name = document["name"].GetString();
   int age = document["age"].GetInt();
   bool isStudent = document["isStudent"].GetBool();

   // Output the extracted properties
   printf("Name: %s\n", name);
   printf("Age: %d\n", age);
   printf("Is Student: %s\n", isStudent ? "true" : "false");

   return 0;
}
```

## Conclusion

JSON serialization and deserialization are essential tasks in web development and API integrations. In this blog post, we explored two widely used JSON libraries in C++: cJSON and RapidJSON. Both libraries provide easy-to-use APIs for manipulating JSON data in C++ programs. Whether you choose cJSON or RapidJSON largely depends on your specific requirements and preferences.

#JSONSerialization #C++