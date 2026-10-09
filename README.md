<div align="center">
  <img src="NginxLogo.svg" alt="NGINX Logo" width="30%" height="50%"/>

<h1>NGINX Documentation</h1>
</div>

## Description

This documentation provides a comprehensive, hands-on reference for NGINX architecture, core configuration directives, and production traffic management. It covers foundational web serving, reverse proxying, Layer 7 load balancing with health checks, HTTP/2 protocol adoption, and performance optimization techniques such as microcaching and response compression. Additionally, it details operational security controls, including leaky-bucket rate limiting, IP-based access restrictions, and SSL/TLS termination.

---

## Disclaimer

> [!NOTE]
> This documentation was created solely for educational purposes to assist learners in studying, reviewing, and quickly revisiting core concepts. Documenting technical topics serves as evidence of the effort spent extracting, organizing, and structuring knowledge, while actively improving long-term retention.
>
> This repository is **not** a replacement for the original course, book, or tutorial series. All copyrights, intellectual property rights, teaching materials, topics, and original content belong entirely to the original author, instructor, and publisher. Readers are strongly encouraged to purchase or access the original resource directly via the [Original Course Link](https://www.udemy.com/course/-training/?couponCode=KEEPLEARNING#reviews).
>
> If the original author, instructor, or copyright holder wishes for this repository or any of its contents to be removed, please contact me and I will unhesitatingly comply immediately.
>
> Happy learning :)

---

## Terminologies Reference

This repository includes a dedicated [**`Terminologies.md`**](Terminologies.md) file that contains the most important technical terms, definitions, and concepts covered throughout the documentation. It serves as a quick-reference glossary to reinforce understanding, clarify terminology, and simplify revision when preparing for interviews or technical reviews.

---

## Table of Contents

### Section 01 - Course Introduction
* Introduction to NGINX
  * Course Overview and Modular Approach
  * Core Roles of NGINX
    * Web Server
    * Reverse Proxy
    * Software Load Balancer
  * HTTP Protocol Foundations and Compression
  * Curriculum Scope and Practical Focus
  * Course Support and Certification
* About NGINX Origin
  * Solving the C10K Concurrent Connection Problem
  * Open Source Release and Architecture
  * NGINX Open Source vs NGINX Plus
  * Protocol Support
    * HTTP, TCP, and UDP
    * Mail Proxy
  * Cloud Architectures and Containerized Environments
    * Dockerized Deployments
    * Kubernetes Integration
  * Multifunctional Application Delivery
* NGINX vs Apache Web Server
  * Architectural Comparison
    * Apache Process-Driven Model
    * NGINX Event-Driven Asynchronous Model
  * Module Management and Resource Consumption
  * Concurrency and High-Traffic Performance
  * Static vs Dynamic Content Processing
  * Configuration Models
    * Centralized Configuration in NGINX
    * Distributed Per-Directory Configuration in Apache (.htaccess)
  * Request Interpretation and URI Matching
  * Hybrid Architecture: NGINX Frontend with Apache Backend

### Section 02 - NginX Installation
* Installing NGINX via Package Manager
  * Connecting to the Ubuntu Server
  * APT Package Manager Update and Installation
  * Verifying NGINX Service and Process Model
    * Master Process
    * Worker Processes
  * Exploring Default Configuration and Log Directories
  * Accessing Default Web Page and Verifying HTTP Status Codes
* Building NGINX from Source Code
  * Motivation for Compiling from Source
  * Preparing OS Dependencies on Ubuntu and CentOS
  * Downloading and Extracting NGINX Source Archive
  * Compilation Prerequisites and Toolchains
  * Configuring Build Options
    * Installation Paths for Binaries, Configuration, and Logs
    * PCRE, SSL, and System Libraries
  * Compiling with Make and Installation
  * Package Manager vs Source Installation Comparison
* Adding NGINX as an OS Service
  * Service Management with systemd
  * Creating the systemd Unit File
    * Unit Configuration
    * Service Directives and Lifecycle Controls
    * Install Target
  * Reloading systemd Daemon and Verifying Service Status
  * Managing Lifecycle with systemctl
    * Starting, Stopping, and Restarting NGINX
    * Configuration Testing and Service Reloading
  * NGINX Process Signals
  * Enabling Automatic Boot Startup

### Section 03 - HTTP Protocol and Applications
* Types of Network Protocols
  * Protocol Definitions and Communication Models
  * Transport Layer Protocols
    * Transmission Control Protocol (TCP)
    * User Datagram Protocol (UDP)
  * Internet Protocol (IP) and Packet Routing
  * Application Protocols
    * Post Office Protocol (POP3)
    * Simple Mail Transfer Protocol (SMTP)
    * File Transfer Protocol (FTP)
  * Hypertext Transfer Protocol (HTTP) vs Secure HTTP (HTTPS)
* HTTP Protocol Working Model
  * HTTP in the TCP/IP Network Stack
  * Client-Server Architecture and Lifecycle
  * Core HTTP Characteristics
    * Connectionless Model
    * Media Independence
    * Stateless Communication
  * Request Processing Architecture and Execution Stages
  * Static vs Dynamic Content Delivery
* HTTP Requests and Message Elements
  * HTTP Request Structure
  * Request Line Breakdown
    * HTTP Request Methods (GET, POST, PUT, DELETE, CONNECT)
    * Request URI
    * Protocol Version
  * Standard HTTP Request Headers
  * Request Body and Message Delimiters
  * Inspecting Requests via Browser Developer Tools
* HTTP Response Codes
  * Status Code Classification and Purpose
  * 1xx Informational Responses
  * 2xx Successful Responses
    * 200 OK
    * 201 Created
  * 3xx Redirection Responses
    * 301 Moved Permanently
    * 304 Not Modified
  * 4xx Client Errors
    * 400 Bad Request
    * 401 Unauthorized
    * 403 Forbidden
    * 404 Not Found
  * 5xx Server Errors
    * 500 Internal Server Error
    * 502 Bad Gateway
    * 503 Service Unavailable
  * Inspecting and Diagnosing Response Codes in Network Logs

### Section 04 - NginX Configuration & Applications
* NGINX Configuration Terminology
  * Configuration File Structure and Hierarchy
  * Context Levels
    * Main and Global Context
    * Events Context
    * HTTP Context
    * Server Context
    * Location Context
    * Upstream Context
    * Mail Context
  * Directives and Inheritance Rules
  * Worker Process and Connection Sizing
    * worker_processes and CPU Cores
    * worker_connections and System Open File Limits
    * Sizing Calculations Based on CPU and Memory Capacity
* Loading Static Data and Creating Virtual Hosts
  * Creating Server Blocks and Virtual Hosts
  * Configuring server_name and Document Root
  * Safe Configuration Workflow (Testing vs Reloading)
  * MIME Types Handling and Including mime.types
  * Multi-Port Virtual Host Configurations
* Location Block Context and Routing
  * Request URI Matching in Location Blocks
  * Location Matching Modifiers
    * Prefix Match (No Modifier)
    * Exact Match (=)
    * Case-Sensitive Regular Expression (~)
    * Case-Insensitive Regular Expression (~*)
    * Preferential Prefix Match (^~)
  * Modifier Precedence and Evaluation Order
  * Nested Locations and Route Segregation
* Variables in NGINX Configuration
  * Built-in Variables ($args, $arg_name, $hostname, $uri, $request_uri)
  * User-Defined Variables with the set Directive
  * Evaluating Query Parameters in Dynamic Responses
  * Conditional Logic with the if Directive
* Rewrite and Return Directives
  * HTTP Redirection with the return Directive
  * URL Rewriting with the rewrite Directive
  * Return vs Rewrite Differences and Use Cases
  * Capturing Regex Groups and Passing Parameters
* Resource Checking with try_files
  * Validating File and Directory Existence
  * Evaluation Sequence and Fallback Strategies
  * Using $uri and Serving Custom 404 Errors
* Logging Management and Special Logging
  * Access Logging (access.log) and Error Logging (error.log)
  * Log Formatting with log_format
  * Monitoring Logs in Real Time
  * Configuring Dedicated Access Logs per Location
  * Disabling Access Logging for Specific Resources
* Handling Dynamic Requests with FastCGI and PHP-FPM
  * Static vs Dynamic Request Processing Flow
  * PHP-FPM Installation and Service Verification
  * FastCGI Parameters and Directives (fastcgi_pass, fastcgi_index)
  * Unix Domain Sockets vs TCP Sockets
  * Diagnosing 502 Bad Gateway and Socket Permission Issues
* Performance Optimization: Workers and Connections
  * Master and Worker Process Operational Mechanics
  * Configuring worker_processes and auto Detection
  * Tuning worker_connections in the Events Context
  * Adjusting Operating System File Descriptor Limits
* Performance Optimization: Buffers, Timeouts, and Zero-Copy
  * Client Request Buffering
    * client_body_buffer_size
    * client_header_buffer_size
    * client_max_body_size
    * large_client_header_buffers
  * Request and Connection Timeouts
    * client_body_timeout
    * client_header_timeout
    * keepalive_timeout
    * send_timeout
  * Kernel Zero-Copy Data Transfer Directives
    * sendfile
    * tcp_nopush
    * tcp_nodelay
* Adding Modules in NGINX
  * Static vs Dynamic Module Architecture
  * Inspecting Available Dynamic Modules
  * Compiling and Installing Modules (Image Filter Module)
  * Loading Modules with load_module Directive
  * Configuring Module Directives in Location Blocks

### Section 05 - NginX Reverse Proxy
* Introduction to Reverse Proxy
  * Reverse Proxy Concepts and Architecture
  * Forward Proxy vs Reverse Proxy
  * Core Benefits
    * Load Balancing
    * Backend Protection and Security
    * Caching and Acceleration
    * SSL/TLS Termination
* Configuring NGINX as a Reverse Proxy
  * Multi-Server Architecture Setup
  * Configuring proxy_pass Directives
  * Reverse Proxying to Static and Dynamic Applications
  * Port-Based and Path-Based Upstream Routing
  * Verifying Traffic Flow Across Upstream Access Logs
* Preserving Client Identity with Real IP Directives
  * Client IP Masking Problem in Reverse Proxies
  * Configuring proxy_set_header
    * X-Real-IP Header
    * X-Forwarded-For Header
  * Compiling and Enabling the http_realip_module
  * Defining Custom Log Formats to Track Origin Client IPs

### Section 06 - NginX Performance Management
* Client-Side Caching in NGINX
  * Browser and Client Caching Mechanisms
  * Cache-Control Header Directives (public, private, max-age)
  * Expires Header and Header Priority Rules
  * Setting Expirations with the expires Directive
  * Cache Strategy for Static Assets vs HTML Content
* Server-Side Response Compression with Gzip
  * Bandwidth Reduction and Page Speed Optimization
  * Enabling Gzip with gzip Directive
  * Configuring Compression Levels (gzip_comp_level)
  * Specifying Target MIME Types (gzip_types)
  * Compression Thresholds with gzip_min_length
  * Verifying Content-Encoding Headers and Avoiding Double Compression
* Microcaching Dynamic Content in NGINX
  * Dynamic Content Types (Shared vs Personalized)
  * Microcaching Architecture and Benefits
  * Configuring FastCGI Cache Path (fastcgi_cache_path)
    * Storage Hierarchy and levels Parameter
    * Shared Memory Zone (keys_zone)
    * Inactive Timeout and Maximum Storage Size
  * Defining the Cache Key with fastcgi_cache_key
* Hands-on Microcaching Implementation and Benchmarking
  * Configuring FastCGI Cache in Location Blocks
  * Cache Validity Durations with fastcgi_cache_valid
  * Load Testing and Benchmarking with ApacheBench (ab)
  * Tracking Cache Status with X-Cache Header (HIT vs MISS)
  * Inspecting Disk Cache Hierarchy and Handling systemd PrivateTmp

### Section 07 - Manage Security in NginX
* Enabling Secure Connections with HTTPS
  * SSL/TLS Fundamentals and Asymmetric/Symmetric Cryptography
  * Step-by-Step SSL Handshake Lifecycle
  * Generating Private Keys and Certificates with OpenSSL
  * Configuring HTTPS in NGINX
    * SSL Listening Port 443
    * ssl_certificate and ssl_certificate_key Directives
  * Handling Self-Signed Certificate Warnings in Modern Browsers
* HTTP/2 Protocol Architecture
  * HTTP/1.1 Inefficiencies and Head-of-Line Blocking
  * HTTP/2 Core Features
    * Binary Framing Layer
    * Multiplexed Streams over a Single TCP Connection
    * Stateful HPACK Header Compression
    * Server Push Mechanism
  * Performance Gains for High-Latency and Mobile Connections
* Enabling and Validating HTTP/2
  * Building NGINX with http_v2_module
  * Configuring HTTP/2 in Server Blocks
  * Validating Protocol Negotiation with Browser Tools and curl
* Traffic Shaping and DoS Protection with Rate Limiting
  * DoS Mitigation and Brute-Force Defense Concepts
  * Leaky Bucket Algorithm Mechanics
  * Defining Rate-Limiting Zones with limit_req_zone
    * Selecting Rate-Limiting Keys (Binary IP)
    * Shared Memory Allocation and Rate Limits (r/s, r/m)
  * Applying Rate Limits with limit_req
  * Managing Bursts and Queues (burst Parameter)
  * Immediate Processing with nodelay Parameter
  * Stress Testing and Validating Rate Limits with Siege

### Section 08 - NginX As Load Balancer
* Load Balancing Fundamentals
  * Traffic Distribution and High Availability Architecture
  * Failover and Auto-Scaling Concepts
  * Load-Balancing Algorithms
    * Round Robin
    * Least Connections
    * Least Response Time and Bandwidth
    * IP Hash
  * Session Persistence Principles
  * Hardware vs Software Load Balancers
  * Defining Server Pools in the upstream Context
* Configuring a Simple Load Balancer
  * Multi-Server Lab Architecture and Environment
  * Defining Backend Pools in upstream Blocks
  * Forwarding Requests via proxy_pass
  * Verifying Alternating Responses with curl
  * Tracking Requests Across Backend Access Logs
* Default Health Checks in NGINX
  * TCP vs HTTP Health Checks
  * Passive vs Active Health Checks
  * Default Failure Detection and Request Rerouting
  * Observing Backend Downtime and Automatic Traffic Rerouting
* Passive Health Checks Configuration
  * Passive Health-Checking Operational Flow
  * Configuring Parameters
    * fail_timeout Parameter
    * max_fails Parameter
  * Practical Lab: Simulating Server Outages and Recovery
  * Single-Server Exception and Threshold Tuning
* Active Health Checks in NGINX
  * Active vs Passive Monitoring Differences
  * The health_check Directive and NGINX Plus Architecture
  * Configuring Active Parameters (interval, fails, passes, uri, port)
  * Defining Custom Health Conditions with match Blocks
    * Status Code Verification
    * Response Body Matching
    * Header Inspection
  * High-Availability Logging and Monitoring Best Practices

### Section 09 - Cache System
* Verifying Server-Side Resource Modifications
  * Cache Invalidation and Stale Content Challenges
  * Conditional HTTP Requests and Revalidation
  * Conditional Headers
    * If-Modified-Since Request Header
    * Last-Modified Response Header
  * Resolving Status Codes: 200 OK vs 304 Not Modified
  * Practical Lab: Validating Cache Freshness and Timestamp Modifications

### Section 10 - NginX Access Control
* IP-Based Access Control and Resource Protection
  * IP Whitelisting and Blacklisting Principles
  * Directives: allow and deny
  * Context Scope (http, server, location)
  * Applying CIDR Subnet Notation
  * Restricting Access to Specific Endpoints and Static File Types
  * Managing Multi-IP Access Lists with External include Files
  * Diagnosing and Troubleshooting HTTP 403 Forbidden Responses

  
### To-Do

#### Read + Doc in Term. (No Practice Needed)
[13. Types of Protocols.md](Course%20Content/Section%2003%20-%20HTTP%20Protocol%20and%20Applications/13.%20Types%20of%20Protocols.md)
[14. HTTP Protocol Working Model.md](Course%20Content/Section%2003%20-%20HTTP%20Protocol%20and%20Applications/14.%20HTTP%20Protocol%20Working%20Model.md)
[15. HTTP Requests & Elements.md](Course%20Content/Section%2003%20-%20HTTP%20Protocol%20and%20Applications/15.%20HTTP%20Requests%20%26%20Elements.md)
[16. HTTP Response Codes.md](Course%20Content/Section%2003%20-%20HTTP%20Protocol%20and%20Applications/16.%20HTTP%20Response%20Codes.md)

#### Read + Practice + Doc in Term. (Easy)
[23. Lab - NGINX Logging Files & Special Logging.md](Course%20Content/Section%2004%20-%20NginX%20Configuration%20%26%20Applications/23.%20Lab%20-%20NGINX%20Logging%20Files%20%26%20Special%20Logging.md)

#### Read + Practice + Doc in Term. (Easy)
[43. Load Balancer Introduction.md](Course%20Content/Section%2008%20-%20NginX%20As%20Load%20Balancer/43.%20Load%20Balancer%20Introduction.md)
[44. Simple Load Balancer with NGINX.md](Course%20Content/Section%2008%20-%20NginX%20As%20Load%20Balancer/44.%20Simple%20Load%20Balancer%20with%20NGINX.md)
[45. Default HealthChecks in NGINX Load Balancer.md](Course%20Content/Section%2008%20-%20NginX%20As%20Load%20Balancer/45.%20Default%20HealthChecks%20in%20NGINX%20Load%20Balancer.md)
[46. Passive HealthCheck In NGINX.md](Course%20Content/Section%2008%20-%20NginX%20As%20Load%20Balancer/46.%20Passive%20HealthCheck%20In%20NGINX.md)
[47. Active Health Check in NGINX.md](Course%20Content/Section%2008%20-%20NginX%20As%20Load%20Balancer/47.%20Active%20Health%20Check%20in%20NGINX.md)

#### Read (No Practice Needed)
[51. Verify Cache File Modified at Server.md](Course%20Content/Section%2009%20-%20Cache%20System/51.%20Verify%20Cache%20File%20Modified%20at%20Server.md)

#### Read + Practice + Doc in Term. (Easy)
[52. Allow and Restrict IP in NGINX.md](Course%20Content/Section%2010%20-%20NginX%20Access%20Control/52.%20Allow%20and%20Restrict%20IP%20in%20NGINX.md)
[53. Limit Access to Resources in NGINX.md](Course%20Content/Section%2010%20-%20NginX%20Access%20Control/53.%20Limit%20Access%20to%20Resources%20in%20NGINX.md)[Section 08 - NginX As Load Balancer](Course%20Content/Section%2008%20-%20NginX%20As%20Load%20Balancer)