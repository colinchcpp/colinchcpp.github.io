---
layout: post
title: "Network programming with C++ OOP"
description: " "
date: 2023-09-13
tags: [include, networkprogramming]
comments: true
share: true
---

In today's interconnected world, network programming plays a crucial role in building communication applications. C++ is a powerful and widely used programming language that provides robust support for network programming. In this blog post, we will explore how to use C++ with an Object-Oriented Programming (OOP) approach to develop network applications.

## Understanding Object-Oriented Programming (OOP)

Object-Oriented Programming is a programming paradigm that organizes the code around objects, which are instances of classes. In C++, we can leverage OOP principles to design our network applications in a modular and scalable manner.

## Setting Up a Basic TCP Server

To begin with, let's create a basic TCP server using C++ with OOP approach. Here's an example of how we can achieve this:

```cpp
#include <iostream>
#include <cstdlib>
#include <cstring>
#include <unistd.h>
#include <arpa/inet.h>
#include <sys/socket.h>

class TCPServer {
private:
    int serverSocket;
    int clientSocket;
    struct sockaddr_in serverAddress;
    struct sockaddr_in clientAddress;
    
public:
    TCPServer(int port) {
        serverSocket = socket(AF_INET, SOCK_STREAM, 0);
        if (serverSocket < 0) {
            std::cerr << "Error creating server socket!" << std::endl;
            exit(EXIT_FAILURE);
        }

        memset(&serverAddress, 0, sizeof(serverAddress));
        serverAddress.sin_family = AF_INET;
        serverAddress.sin_addr.s_addr = INADDR_ANY;
        serverAddress.sin_port = htons(port);

        if (bind(serverSocket, (struct sockaddr*)&serverAddress, sizeof(serverAddress)) < 0) {
            std::cerr << "Error binding server socket!" << std::endl;
            exit(EXIT_FAILURE);
        }

        listen(serverSocket, 3);
        std::cout << "Server listening on port " << port << std::endl;
    }

    void acceptConnection() {
        socklen_t clientAddressLength = sizeof(clientAddress);
        clientSocket = accept(serverSocket, (struct sockaddr*)&clientAddress, &clientAddressLength);
        if (clientSocket < 0) {
            std::cerr << "Error accepting connection!" << std::endl;
            exit(EXIT_FAILURE);
        }
        std::cout << "New client connected: " << inet_ntoa(clientAddress.sin_addr) << std::endl;
    }

    void closeConnection() {
        close(clientSocket);
        close(serverSocket);
    }
};

int main() {
    TCPServer server(8080);
    server.acceptConnection();
    server.closeConnection();
    return 0;
}
```

In the above code, we define a `TCPServer` class that encapsulates the functionalities related to a TCP server. We create a server socket, bind it to a specific port, and listen for incoming connections. When a client connects, we accept the connection and display the client's IP address. Finally, we provide a method to close the server and client connections.

## Conclusion

By leveraging the power of Object-Oriented Programming (OOP), we can design and implement network applications in C++ in a more organized and scalable way. This enables us to build robust and efficient network programs that can handle multiple connections and communicate seamlessly.

#cpp #networkprogramming