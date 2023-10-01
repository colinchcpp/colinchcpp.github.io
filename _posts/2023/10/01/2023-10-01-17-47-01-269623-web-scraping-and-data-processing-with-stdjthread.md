---
layout: post
title: "Web scraping and data processing with `std::jthread`"
description: " "
date: 2023-10-01
tags: [include, include]
comments: true
share: true
---

## What is `std::jthread`?

`std::jthread` is a new class introduced in C++20 that provides a convenient way to manage threads. It is similar to `std::thread`, but it has a few advantages over the older class. One key advantage is that `std::jthread` handles the thread lifetime automatically. When a `std::jthread` object goes out of scope, it will join the associated thread if it's still joinable. This ensures that the thread is properly cleaned up, avoiding resource leaks.

## Web scraping with `std::jthread`

Web scraping involves fetching data from websites and extracting relevant information. With `std::jthread`, we can easily parallelize the scraping process to speed up data collection.

To get started, we'll need the help of a networking library like Boost.Beast or cURL to fetch the web page content. Let's assume we are using Boost.Beast for this example.

```cpp
#include <boost/beast.hpp>
#include <iostream>
#include <string>
#include <vector>
#include <span>
#include <jthread>

namespace beast = boost::beast;
using tcp = boost::asio::ip::tcp;

void scrapeUrl(const std::string& url)
{
    // Fetch the web page content using Boost.Beast
    beast::tcp_stream stream;
    // ... implementation details omitted

    // Process the fetched content
    // ... implementation details omitted
}

int main()
{
    std::vector<std::string> urls = {"https://example.com", "https://google.com", "https://stackoverflow.com"};

    std::vector<std::jthread> threads;
    for (const std::string& url : urls) {
        threads.emplace_back(scrapeUrl, url);
    }

    // Wait for all threads to finish
    for (std::jthread& thread : threads) {
        thread.join();
    }

    return 0;
}
```

In the above example, we define a `scrapeUrl` function that takes a URL as input and fetches the web page content using Boost.Beast. Within the `main` function, we create a vector of `std::jthread` objects, each associated with a URL to scrape. The `scrapeUrl` function is called in a separate thread for each URL using `std::jthread`'s constructor.

Using this approach, we can easily parallelize the web scraping process and fetch multiple URLs concurrently. With `std::jthread`, we don't have to worry about explicitly joining or detaching threads, as the cleanup is handled automatically when the `std::jthread` objects go out of scope.

## Data processing with `std::jthread`

Once we have the scraped data, we can further process it using `std::jthread`. Let's consider an example where we want to count the number of occurrences of a specific word in the scraped content.

```cpp
#include <iostream>
#include <string>
#include <jthread>
#include <algorithm>

int countOccurrences(const std::string& content, const std::string& word)
{
    int count = 0;
    std::string lowerContent = content;
    std::transform(lowerContent.begin(), lowerContent.end(), lowerContent.begin(), ::tolower);
    std::string lowerWord = word;
    std::transform(lowerWord.begin(), lowerWord.end(), lowerWord.begin(), ::tolower);

    size_t pos = 0;
    while ((pos = lowerContent.find(lowerWord, pos)) != std::string::npos) {
        count++;
        pos += lowerWord.length();
    }

    return count;
}

int main()
{
    std::string scrapedContent = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed sed sagittis libero, eu condimentum tellus. Sed eu facilisis neque, ac finibus enim.";

    std::vector<std::pair<std::string, std::string>> wordOccurrences = {
        {"Lorem", ""},
        {"ipsum", ""},
        {"libero", ""}
    };

    std::vector<std::jthread> threads;
    for (auto& [word, count] : wordOccurrences) {
        threads.emplace_back([&] {
            count = countOccurrences(scrapedContent, word);
        });
    }

    // Wait for all threads to finish
    for (std::jthread& thread : threads) {
        thread.join();
    }

    // Print the word occurrences
    for (auto& [word, count] : wordOccurrences) {
        std::cout << word << ": " << count << " occurrences" << std::endl;
    }

    return 0;
}
```

In this example, we define a `countOccurrences` function that takes a string content and a word as input and counts the number of occurrences of that word in the content. We create a vector of word occurrences, where each pair consists of a word and an initially empty count.

Within the `main` function, we create `std::jthread` objects for each word and use a lambda function to update the count of each word occurrence. After joining all the threads, we print the word occurrences.

The use of `std::jthread` in this scenario allows us to process different parts of the scraped content concurrently, improving performance.

## Conclusion

With the addition of `std::jthread` to the C++ standard library, handling concurrent tasks like web scraping and data processing has become easier and more efficient. It provides automatic thread cleanup, simplifying code and preventing resource leaks. In this blog post, we explored how to leverage `std::jthread` to parallelize web scraping and data processing tasks. By utilizing concurrent programming techniques, we can improve the performance of our applications and deliver faster results. #web #scraping