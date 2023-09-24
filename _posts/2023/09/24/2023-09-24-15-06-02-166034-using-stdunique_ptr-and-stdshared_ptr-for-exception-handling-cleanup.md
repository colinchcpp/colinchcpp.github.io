---
layout: post
title: "Using `std::unique_ptr` and `std::shared_ptr` for exception-handling cleanup"
description: " "
date: 2023-09-24
tags: [exceptionhandling]
comments: true
share: true
---

`std::unique_ptr` is designed for exclusive ownership of dynamically allocated objects. It takes care of deleting the object when it goes out of scope, whether that happens through normal program flow or due to an exception being thrown. This makes it particularly useful for managing resources that should be cleaned up as soon as they are no longer needed.

Here's an example of using `std::unique_ptr` to manage a dynamically allocated resource:

```cpp
void someFunction() {
    std::unique_ptr<Resource> resource(new Resource());
    
    // Use the resource...
    
    // If an exception is thrown here, the resource will be safely deleted
    
    // Clean up the resource manually if needed
    // resource.reset();
}
```

In the example above, the `std::unique_ptr` `resource` is created and initialized with a new instance of the `Resource` class. The pointer takes ownership of the dynamically allocated object. When `resource` goes out of scope, it will automatically delete the `Resource` object, regardless of whether an exception was thrown or not.

`std::shared_ptr`, on the other hand, allows for multiple ownership of a dynamically allocated object. It keeps track of the number of references to the object and deletes it when the last reference goes out of scope. This can be useful when you need to share ownership of a resource across multiple parts of your code.

Here's an example of using `std::shared_ptr` to manage a dynamically allocated resource:

```cpp
void someFunction() {
    std::shared_ptr<Resource> sharedResource(new Resource());
    
    // Use the shared resource...
    
    // If an exception is thrown here, the shared resource will be safely deleted when all references are gone
    
    // Clean up the shared resource manually if needed
    // sharedResource.reset();
}
```

In the example above, the `std::shared_ptr` `sharedResource` is created and initialized with a new instance of the `Resource` class. Multiple copies of `sharedResource` can be made, and the dynamically allocated object will only be deleted when the last reference is gone.

Using `std::unique_ptr` and `std::shared_ptr` for exception-handling cleanup can greatly simplify resource management in C++, ensuring that resources are properly cleaned up in case of an exception. By leveraging these smart pointer types, you can write more robust and reliable code. #cpp #exceptionhandling