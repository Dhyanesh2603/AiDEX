# AiDEX ⚡

> **High-Performance Autonomous AI Developer Environment, Workspace Daemon & Desktop Suite**

[![Rust](https://img.shields.io/badge/Rust-1.85%2B-DEA584?style=for-the-badge&logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Tauri](https://img.shields.io/badge/Tauri-v2-24C8D8?style=for-the-badge&logo=tauri&logoColor=white)](https://tauri.app/)
[![Bun](https://img.shields.io/badge/Bun-1.3%2B-FBF0DF?style=for-the-badge&logo=bun&logoColor=black)](https://bun.sh/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

---

## Overview

**AiDEX** is a next-generation local AI developer platform combining a high-performance **Rust workspace daemon** with a hardware-accelerated **Tauri desktop shell** and headless CLI toolchain. Engineered for deterministic local session execution, workspace virtualization, and high-frequency event streaming between autonomous agent drivers and local codebases.

```
                  ┌────────────────────────────────────────┐
                  │          AiDEX Desktop (Tauri)         │
                  └──────────────────┬─────────────────────┘
                                     │ IPC / RPC
                  ┌──────────────────▼─────────────────────┐
                  │         aidexd (Rust Daemon)           │
                  └──────┬───────────┬──────────────┬──────┘
                         │           │              │
           ┌─────────────▼──┐ ┌──────▼──────┐ ┌─────▼──────────┐
           │ crates/storage │ │ crates/host │ │ crates/sessions│
           └────────────────┘ └─────────────┘ └────────────────┘
```

---

## Key Architecture & Crates

AiDEX is structured as a unified multi-crate Cargo workspace paired with a Bun-managed TypeScript frontend monorepo:

| Crate | Purpose |
| :--- | :--- |
| **`crates/aidexd`** | Central background orchestration daemon managing local agent execution loops. |
| **`crates/aidex-cli`** | Developer CLI powered by `clap` for terminal interactions, session attach, and headless runs. |
| **`crates/core`** | Domain types, AST protocol definitions, and telemetry primitives. |
| **`crates/sessions`** | Stateful session lifecycle manager with crash-safe transaction boundaries. |
| **`crates/storage`** | Fast local key-value and snapshot persistence engine. |
| **`crates/drive`** | Virtualized filesystem driver with sandbox confinement. |
| **`crates/host`** | OS process isolation and IPC socket server. |
| **`apps/desktop`** | Cross-platform Tauri desktop client with real-time streaming visualization. |

---

## Getting Started

### Prerequisites
- **Rust Toolchain**: `1.85+` (`cargo`, `rustc`)
- **Bun**: `1.3.14+`
- **Node.js**: `22+` (for TypeScript build verification)

### Installation & Development

```bash
# Clone the repository
git clone https://github.com/Dhyanesh2603/AiDEX.git
cd AiDEX

# Install workspace dependencies
bun install

# Run the developer CLI
bun run dev:cli

# Launch the Tauri desktop GUI in dev mode
bun run dev:desktop
```

---

## Code Quality & Safety
- **Strict Concurrency**: Zero `unsafe` blocks permitted via `#![forbid(unsafe_code)]` at the workspace root.
- **Strict Clippy**: Configured with `#![warn(clippy::all)]` for idiomatic, production-grade memory safety.

---

## License
Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for details.
