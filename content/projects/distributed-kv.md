---
title: "Distributed Key-Value Store"
date: 2026-01-15T12:00:00Z
description: "An implementation of a distributed KV store using the Raft consensus algorithm."
github: "https://github.com/example/distributed-kv"
demo: "https://demo.example.org/kv"
---

This project implements a distributed, linearizable key-value store. 

### Key Features
- **Raft Consensus:** Built from scratch to handle leader election and log replication.
- **gRPC API:** High-performance communication between nodes.
- **Persistence:** Custom storage engine based on append-only logs.

```go
func (s *Server) Put(key string, value string) error {
    // Propose to Raft log
    return s.raft.Propose(Command{Op: "Put", Key: key, Value: value})
}
```
