# Zero-Trust Node.js Microservices — Benchmarking Suite

> Research implementation and benchmarking code for the paper:  
> **"Evaluating Latency Overhead and Identity Consistency Mechanisms in
> Zero-Trust Node.js Microservice Environments"**  

---

## What This Repository Contains

This repository contains the complete source code for the experimental
setup described in the paper. It includes two independently runnable
versions of the same microservice system — a baseline (implicit trust)
and a Zero Trust implementation — along with all Autocannon benchmark
scripts used to produce the data in Tables 1 and 2.

---

## System Overview

The architecture consists of three Node.js services:

- **API Gateway** — entry point for all external requests. In the Zero
  Trust version, this is where RS256 token signing happens.
- **Product Service** — handles GET /product/:id (read-heavy endpoint)
- **Cart Service** — handles POST /checkout (write-heavy endpoint)

and a directory containing the results of AutoCannon tool.

Two trust models are implemented side by side:

| Model | Description |
|---|---|
| Baseline (Implicit Trust) | Gateway forwards requests with raw HTTP headers. No internal token generation. |
| Zero Trust | Gateway issues a short-lived RS256-signed JWT per request. Downstream services verify signature before processing. |

---

## Requirements

- Node.js v20 (LTS)
- npm v9+
- Autocannon (`npm install -g autocannon`)

No external database or cloud infrastructure required.
All services run on localhost via loopback interface.

---

## Setup

```bash
