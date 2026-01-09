# Distributed Web Crawler System

![Project Status](https://img.shields.io/badge/Status-Active-success)
![Architecture](https://img.shields.io/badge/Architecture-Microservices-blueviolet)
![Language](https://img.shields.io/badge/Stack-Python%20|%20Node.js-blue)

## 📖 Overview
This project is a modular, distributed web crawling system designed to handle [Insert specific goal, e.g., high-volume data extraction / specific site monitoring]. 

Unlike a monolithic application, this system is decoupled into **four distinct microservices** to ensure scalability, fault tolerance, and separation of concerns. The architecture separates the heavy computational logic (crawling) from the user interface and API management.

## 🏗 System Architecture
The system operates on a pipeline architecture:

1.  **[**WebCrawler_frontend**](https://github.com/Fanboyingeneral/WebCrawler_frontend):** User defines crawl targets and views results.
2.  **[**WebCrawler_client_side_backend**](https://github.com/Fanboyingeneral/WebCrawler_client_side_backend):** Can be used to use the client machine as the host for carrying out the crawl instead of a remote server.
3.  **[**WebCrawler_backend**](https://github.com/Fanboyingeneral/WebCrawler_backend):** Manages the task queue, database operations, and orchestration.
4.  **[**WebCrawler_crawler_engine**](https://github.com/Fanboyingeneral/WebCrawler_crawler_engine):** The isolated Python worker that executes the actual scraping logic.



## 🏗 System Architecture
The system employs a **Hybrid Execution Model**, allowing crawl jobs to be executed either remotely on the server or locally on the client's machine. This is handled by the specialized `Client Side Backend`.

* **Remote Mode:** Standard server-side crawling using the distributed Python engine.
* **Local/Client Mode:** The `Client Side Backend` turns the user's machine into a temporary crawl node, bypassing server-side IP restrictions and distributing the network load.
