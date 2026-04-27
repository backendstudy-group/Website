---
title: "Distributed Key-Value Store"
date: 2026-01-15T12:00:00Z
description: "An implementation of a distributed KV store using the Raft consensus algorithm."
summary: "A distributed, linearizable key-value store built from scratch — featuring Raft consensus, gRPC transport, and a custom append-only storage engine."
github: "https://github.com/example/distributed-kv"
demo: "https://demo.example.org/kv"
tags: ["Go", "Raft", "gRPC", "Distributed Systems"]
features:
  - title: "Raft Consensus"
    description: "Built from scratch to handle leader election and log replication across nodes."
  - title: "gRPC API"
    description: "High-performance, strongly-typed communication between cluster nodes."
  - title: "Persistence"
    description: "Custom storage engine based on append-only logs for crash recovery."
code: |
  func (s *Server) Put(key, value string) error {
    return s.raft.Propose(Command{
      Op:    "Put",
      Key:   key,
      Value: value,
    })
  }
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
