# From Scratch

Systems engineering in C and Rust, targeting the Linux kernel primitives that power modern infrastructure: memory management, process lifecycles, non-blocking I/O, sockets, and OS isolation.

Core utilities, servers, runtimes, and proxies implemented from scratch—first in C to interface directly with low-level kernel APIs, then in Rust for memory-safe, high-concurrency systems design.



## Core Focus Areas

* **C & Memory Semantics:** Manual heap allocation, raw pointer manipulation, custom data structures, and predictable cache/memory layout.
* **Linux Kernel Interfaces:** System calls, process control, file descriptors, POSIX signal dispatch, network stacks, namespaces, and cgroups.
* **Rust Systems Architecture:** Zero-cost abstractions, strict ownership invariants, lock-free/safe concurrency, and asynchronous I/O runtimes.
* **Infrastructure Internals:** Reverse-engineering the mechanisms underlying Docker, Nginx, and modern orchestration engines.




## Projects

#### Implemented in C

**Unix Core Utilities**:
Deterministic re-implementations of `cat`, `wc`, `head`, `tail`, and `grep` matching standard POSIX behavior.
* **Focus:** Unbuffered vs. buffered file I/O, chunk-based streaming, POSIX argument parsing, and standardized exit codes.

**Data Structures & Memory Library**:
A reusable, zero-dependency C library providing core abstract data types, topped with a cache eviction engine.
* **Components:** Dynamic array, doubly-linked list, stack, queue, circular ring buffer, hash table (open addressing), binary search tree, binary min/max heap, and an LRU cache.
* **Focus:** Pointer arithmetic, cache locality, explicit allocation lifecycles, and algorithmic complexity guarantees.

**POSIX Unix Shell**:
An interactive command-line interpreter supporting command pipelines, stream redirection, and process control.
* **Focus:** `fork(2)`, `execve(2)`, multi-stage anonymous pipes (`pipe(2)`), signal handling (`SIGINT`, `SIGTSTP`), and process group management.

**Work-Stealing / Task Thread Pool**:
A concurrent thread pool designed to process high-throughput CPU- and I/O-bound jobs (such as parallel multi-file cryptographic hashing) with linear scaling.
* **Focus:** `pthreads`, mutual exclusion (`pthread_mutex`), condition variables (`pthread_cond`), worker thread lifecycle, and race condition prevention.

**Event-Driven HTTP/1.1 Server**:
A single-threaded, high-concurrency static web server capable of servicing thousands of simultaneous connections using an event-driven reactor loop.
* **Focus:** Non-blocking BSD sockets, Linux `epoll(7)` edge/level-triggered notifications, state-machine HTTP parsing, and zero-copy response delivery.

---

#### Implemented in Rust

**High-Throughput Async Chat Server**:
A real-time, multi-client messaging server featuring dynamic room routing, client state isolation, and peer broadcasting.
* **Focus:** `tokio` runtime, async/await event mechanics, multi-producer multi-consumer (`mpsc`/`broadcast`) channels, and graceful connection teardown.

**Container Isolation Runtime**:
A minimal OCI-like container execution engine that runs isolated userspace workloads with constrained system access.
* **Focus:** Linux namespaces (`CLONE_NEWPID`, `CLONE_NEWNET`, `CLONE_NEWNS`), cgroups v2 resource quotas (memory/CPU limits), `pivot_root(2)`, `overlayfs` mounts, and virtual ethernet (`veth`) pair networking.

**Layer 7 Reverse Proxy & Load Balancer**:
An infrastructure proxy featuring round-robin and least-connections routing, upstream health checks, and runtime observability.
* **Focus:** HTTP/1.1 stream forwarding, connection pooling, non-disruptive hot configuration reloads, circuit breakers, and throughput benchmarking against Nginx.



## References & Standards

* **[CS50x](https://cs50.harvard.edu/x/):** *CS50x Lectures*
* **[POSIX.1-2017 & Linux API](https://man7.org/tlpi/):** *The Linux Programming Interface* (Michael Kerrisk)
* **[Systems Architecture](https://pages.cs.wisc.edu/~remzi/OSTEP/):** *Operating Systems: Three Easy Pieces* (Arpaci-Dusseau)
* **[Network Systems](https://beej.us/guide/bgnet/):** *Beej's Guide to Network Programming*
* **[Rust Internals](https://doc.rust-lang.org/book/):** *The Rust Programming Language* & The Tokio Reference Documentation
