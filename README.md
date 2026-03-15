# ConcurrencyLAB

A comprehensive Java project demonstrating three different server concurrency models: Single-threaded, Multithreaded, and Thread Pool implementations. This repository serves as an educational resource for understanding how different concurrency approaches affect server performance and scalability.

## 📋 Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Server Implementations](#server-implementations)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Performance Comparison](#performance-comparison)
- [Key Concepts](#key-concepts)
- [Requirements](#requirements)
- [Contributing](#contributing)

## 🎯 Overview

This project implements a simple TCP server in three different ways to illustrate the evolution of server architectures and their impact on handling concurrent client connections. Each implementation showcases different approaches to managing client requests:

1. **Single-threaded**: Handles one client at a time (blocking)
2. **Multithreaded**: Creates a new thread for each client connection
3. **Thread Pool**: Uses a fixed pool of threads to handle multiple clients efficiently

## 📁 Project Structure

```
multithreading-server/
├── SingleThreaded/
│   ├── Server.java          # Single-threaded server implementation
│   └── Client.java          # Client for single-threaded server
├── Multithreaded/
│   ├── Server.java          # Multithreaded server implementation
│   └── Client.java          # Client for multithreaded server
└── ThreadPool/
    └── Server.java          # Thread pool-based server implementation
```

## 🔧 Server Implementations

### 1. Single-threaded Server

**Location**: `SingleThreaded/Server.java`

**Characteristics**:
- Handles one client connection at a time
- Blocks until current client disconnects before accepting new connections
- Simple but limited scalability
- Port: `8010`

**Pros**:
- Simple implementation
- Low resource overhead
- Predictable behavior

**Cons**:
- Poor scalability
- Blocks on each client connection
- Not suitable for production environments with multiple clients

### 2. Multithreaded Server

**Location**: `Multithreaded/Server.java`

**Characteristics**:
- Creates a new thread for each incoming client connection
- Concurrent handling of multiple clients
- Uses Java's `Consumer<Socket>` functional interface
- Port: `8010`

**Pros**:
- Can handle multiple clients simultaneously
- Better responsiveness than single-threaded approach
- Straightforward thread-per-request model

**Cons**:
- Thread creation overhead for each connection
- Unbounded thread creation can exhaust system resources
- Context switching overhead with many threads

### 3. Thread Pool Server

**Location**: `ThreadPool/Server.java`

**Characteristics**:
- Uses `ExecutorService` with a fixed thread pool
- Configurable pool size (default: 10 threads)
- Reuses threads for multiple client connections
- Port: `8010`

**Pros**:
- Efficient resource utilization
- Bounded resource consumption
- Better performance under high load
- Thread reuse reduces overhead
- Production-ready approach

**Cons**:
- Requires tuning pool size for optimal performance
- Slightly more complex implementation

## 🚀 Getting Started

### Prerequisites

- Java Development Kit (JDK) 8 or higher
- Basic understanding of Java networking and concurrency

### Compilation

Navigate to the desired implementation directory and compile the Java files:

```bash
# Single-threaded
cd SingleThreaded
javac Server.java Client.java

# Multithreaded
cd Multithreaded
javac Server.java Client.java

# Thread Pool
cd ThreadPool
javac Server.java
```

## 💻 Usage

### Running the Servers

**Single-threaded Server**:
```bash
cd SingleThreaded
java Server
```

**Multithreaded Server**:
```bash
cd Multithreaded
java Server
```

**Thread Pool Server**:
```bash
cd ThreadPool
java Server
```

### Running the Client

```bash
cd SingleThreaded  # or Multithreaded
java Client
```

### Testing with Multiple Clients

You can use Jmeter for load testing, start the server on either Single/Multi/ThreadPool and Jmeter simultaneously, then you can vary the incoming request per second and verify


## 📊 Performance Comparison

| Feature | Single-threaded | Multithreaded | Thread Pool |
|---------|----------------|---------------|-------------|
| **Concurrent Clients** | 1 | Unlimited* | Pool Size (10) |
| **Resource Usage** | Low | High (grows with clients) | Fixed |
| **Scalability** | Poor | Moderate | Excellent |
| **Response Time** | High (blocking) | Low | Low |
| **Production Ready** | ❌ | ⚠️ | ✅ |

*Limited by system resources

## 🎓 Key Concepts

### Concurrency Models

1. **Blocking I/O**: Single-threaded approach where the server blocks waiting for each client
2. **Thread-per-request**: Each client gets a dedicated thread
3. **Thread Pool**: Fixed number of worker threads handle requests from a queue

### Java Concurrency Features Demonstrated

- `ServerSocket` and `Socket` for TCP communication
- `Thread` class for creating concurrent execution paths
- `ExecutorService` and `Executors` for thread pool management
- Functional interfaces (`Consumer<Socket>`)
- Try-with-resources for automatic resource management

### Socket Timeouts

All servers implement socket timeouts to prevent hanging:
- Single-threaded: 20 seconds
- Multithreaded: 70 seconds
- Thread Pool: 70 seconds

## ⚙️ Configuration

### Adjusting Thread Pool Size

Edit `ThreadPool/Server.java`:

```java
int poolSize = 100; // Adjust based on your needs
```

Recommended values:
- **CPU-bound tasks**: Number of CPU cores
- **I/O-bound tasks**: Higher values (2-4x CPU cores)

### Changing Port

Update the `port` variable in the respective `Server.java` file:

```java
int port = 8010; // Change to your desired port
```

## 🔍 Requirements

- **Java Version**: JDK 8+
- **Operating System**: Any OS supporting Java (Windows, macOS, Linux)
- **Memory**: Minimal (depends on thread pool size and concurrent clients)

## 🤝 Contributing

Contributions are welcome! Here are some ideas for enhancements:

- Add SSL/TLS support
- Implement HTTP protocol handling
- Add connection pooling for clients
- Create performance benchmarking tools
- Add logging framework
- Implement graceful shutdown
- Add unit tests

## 📝 License

This project is available for educational purposes.

## 🎯 Learning Objectives

By exploring this project, you will learn:

- How to implement TCP servers in Java
- Different approaches to handling concurrent connections
- Trade-offs between various concurrency models
- When to use thread pools vs. thread-per-request
- Best practices for production server implementations

**Happy Learning!** 🚀

For questions or suggestions, feel free to open an issue or submit a pull request.