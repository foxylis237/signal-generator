# signal-generator

Real-time signal monitoring system written in Go.

The project simulates a signal source, streams generated values via gRPC, detects anomalies using statistical analysis, and stores detected events in PostgreSQL.

## Overview

The system consists of two services:

- `server` — generates signal values and exposes them through a gRPC server-streaming API
- `client` — consumes the stream, builds a statistical baseline, detects anomalies, and persists them to PostgreSQL

## Features

- gRPC server streaming
- Protocol Buffers contracts
- real-time stream processing
- statistical anomaly detection
- PostgreSQL persistence
- Docker Compose setup
- Go workspace with separate client and server modules

## Architecture

```text
Signal Generator
        |
        v
gRPC Server Stream
        |
        v
Signal Client
        |
        +-- Baseline Calculation
        +-- Anomaly Detection
        +-- PostgreSQL Storage
```

## Project Structure

```text
.
├── client              # stream consumer, analyzer and storage layer
├── server              # signal generator and gRPC server
├── messages            # protobuf contracts and generated code
├── initdb              # database initialization scripts
├── docker-compose.yml  # local PostgreSQL environment
├── Makefile            # development commands
└── go.work             # Go workspace
```

## Processing Flow

1. The server generates signal values.
2. Values are streamed to the client via gRPC.
3. The client collects an initial baseline sample.
4. Mean value and standard deviation are calculated.
5. New values are compared against the baseline.
6. Detected anomalies are stored in PostgreSQL.

## Stack

- Go
- gRPC
- Protocol Buffers
- PostgreSQL
- pgx
- Docker
- Docker Compose

## Run

```bash
docker compose up -d

make run-server
make run-client
```

## Generate Protobuf

```bash
make generate
```