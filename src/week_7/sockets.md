# Sockets
A socket is an abstract representation of an "endpoint for communication". They
can be either:
- Connection based or connectionless.
- Packet based or stream based.
- Reliable or unreliable.

Sockets are characterised by their domain, type, and transport protocol. 
There are two types of sockets:
1. Connection-based sockets communicate client-server: The server waits for a
connection from the client.
2. Connectionless sockets are peer-to-peer: Each process is symmetric.

Common domains consist of:
- **AF_UNIX**: Address format is UNIX path-name.
- **AF_INET**: Address format is host and port number.

Common types consist of:
- **Virtual circuit**: Received in order transmitted and reliably.
- **Datagram**: Arbitrary order and unreliable.

Common transport protocols consist of:
- TCP/IP (virtual circuit)
- UDP (datagram)

## BSD Socket APIs
- `socket()`: Creates a socket of a given domain, type, and protocol.
- `bind()`: Assigns a name to the socket.
- `listen()`: Specifies the number of pending connections that can be queued for
a server socket.
- `accept()`: Server accepts a connection request from a client.
- `connect()`: Client requests a connection to a server.
- `send(), sendto`: Write to connection.
- `recv(), recvfrom`: Read from connection.
- `shutdown()`: End sending or receiving.
- `close()`: Close a socket and terminate a TCP connection.

## Connection-based Sockets
With connection-based sockets, the server performs the following actions:
- `socket()`
- `bind()`
- `listen()`
- `accept()`
- `send()`
- `recv()`
- `shutdown()`
- `close()`

while the client performs the following actions:
- `socket()`
- `connect()`
- `send()`
- `recv()`
- `shutdown()`
- `close()`

## Connectionless Sockets
Due to communication being symmetric, all devices perform the following actions:
- `socket()`
- `bind()`
- `sendto()`
- `recvfrom()`
- `shutdown()`
- `close()`

## Example
```c
// Server
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

const int NUM_OF_CONNECTIONS = 10;

int main(void) {
    struct sockaddr_in server_addr;
    struct sockaddr_in client_addr;
    socklen_t client_addr_len;
    char buf[1024];

    int fd = socket(AF_INET, SOCK_STREAM, 0);

    if (fd == -1) {
        fprintf(stderr, "[Error] - Failed to create socket.\n");
        return 1;
    }

    server_addr.sin_family = AF_INET;
    // Bind socket so it's able to be connected to from anywhere
    server_addr.sin_addr.s_addr = htonl(INADDR_ANY);
    // Bind socket to port 3000
    server_addr.sin_port = htons(3000);

    if (bind(fd, (struct sockaddr *) &server_addr, sizeof(server_addr)) == -1) {
        fprintf(stderr, "[Error] - Failed to bind socket.\n");
        return 1;
    }

    if (listen(fd, NUM_OF_CONNECTIONS) == -1) {
        fprintf(stderr, "[Error] - Failed to listen for connections.\n");
        return 1;
    }

    int client_fd = accept(fd, (struct sockaddr *) &client_addr, &client_addr_len);

    if (client_fd == -1) {
        fprintf(stderr, "[Error] - Failed to accept connection.\n");
        return 1;
    }

    // Do something with socket
    int bytes_received = recv(client_fd, buf, 1023, 0);

    if (bytes_received == -1) {
        fprintf(stderr, "[Error] - Failed to receive data.\n");
        return 1;
    }

    buf[bytes_received] = '\0';
    printf("Received from client: %s\n", buf);

    if (shutdown(client_fd, SHUT_RDWR) == -1) {
        fprintf(stderr, "[Error] - Failed to shutdown connection.\n");
        return 1;
    }

    close(client_fd);

    close(fd);

    return 0;
}
```

```c
// Client
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

const int NUM_OF_CONNECTIONS = 10;

int main(void) {
    struct sockaddr_in server_addr;
    struct sockaddr_in client_addr;
    socklen_t client_addr_len;
    char buf[1024];
    char *message = "Hello, world!\n";

    int fd = socket(AF_INET, SOCK_STREAM, 0);

    if (fd == -1) {
        fprintf(stderr, "[Error] - Failed to create socket.\n");
        return 1;
    }

    server_addr.sin_family = AF_INET;
    if (inet_pton(AF_INET, "127.0.0.1", &server_addr.sin_addr) != 1) {
        fprintf(stderr, "[Error] - Failed to convert presentation format address to network format.\n");
        return 1;
    }
    server_addr.sin_port = htons(3000);

    if (connect(fd, (struct sockaddr *) &server_add, sizeof(server_addr)) == -1) {
        fprintf(stderr, "[Error] - Failed to connect to server.\n");
        return 1;
    }

    send(fd, message, strlen(message), 0);

    if (shutdown(client_fd, SHUT_RDWR) == -1) {
        fprintf(stderr, "[Error] - Failed to shutdown connection.\n");
        return 1;
    }

    close(fd);

    return 0;
}
```
