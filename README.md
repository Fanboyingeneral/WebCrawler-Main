# Distributed Web Crawler System

![Project Status](https://img.shields.io/badge/Status-Active-success)
![Architecture](https://img.shields.io/badge/Architecture-Microservices-blueviolet)
![Language](https://img.shields.io/badge/Stack-Python%20|%20Node.js-blue)

## 📖 Overview
This project is a modular, distributed web crawling system designed to handle [Insert specific goal, e.g., high-volume data extraction / specific site monitoring]. 

Unlike a monolithic application, this system is decoupled into **four distinct microservices** to ensure scalability, fault tolerance, and separation of concerns. The architecture separates the heavy computational logic (crawling) from the user interface and API management.

## 🏗 System Architecture
The system operates on a pipeline architecture:

1.  **User Interface:** User defines crawl targets and views results.
2.  **Client-Side Backend:** Can be used to use the client machine as the host for carrying out the crawl instead of a remote server.
3.  **Core Backend:** Manages the task queue, database operations, and orchestration.
4.  **Crawler Engine:** The isolated Python worker that executes the actual scraping logic.

## 🏗 System Architecture
The system employs a **Hybrid Execution Model**, allowing crawl jobs to be executed either remotely on the server or locally on the client's machine. This is handled by the specialized `Client Side Backend`.

* **Remote Mode:** Standard server-side crawling using the distributed Python engine.
* **Local/Client Mode:** The `Client Side Backend` turns the user's machine into a temporary crawl node, bypassing server-side IP restrictions and distributing the network load.

```mermaid
graph TD
    subgraph "Client Machine (Local Environment)"
        UI[Frontend UI]
        CSB[Client Side Backend]
    end

    subgraph "Remote Server (Cloud)"
        API[Core Backend API]
        DB[(Database)]
        Worker[Crawler Engine]
    end

    Target((Target Website))

    %% Flows
    UI -->|Mode: Local Crawl| CSB
    UI -->|Mode: Remote Crawl| API
    
    %% Execution Paths
    CSB -->|Executes Request| Target
    API -->|Dispatches Job| Worker
    Worker -->|Executes Request| Target

    %% Data Sync
    CSB -.->|Sync Results| API
    Worker -->|Store Data| DB
    API -->|Read/Write| DB
