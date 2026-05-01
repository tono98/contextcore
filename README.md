# ContextCore

> Decentralized contextual intelligence infrastructure.

ContextCore is an open source infrastructure layer that detects user context in real time, learns behavioral patterns autonomously, and orchestrates specialized AI agents — across any device, any platform, and any use case built on top of it.

---

## Infrastructure, Not a Product

ContextCore is **infrastructure**. It does not solve a specific business problem by itself. It provides the foundational layer that enables others to build context-aware services on top of it.

The distinction matters:

- **ContextCore (infrastructure)** - detects context, learns behavior, manages the DID user profile, orchestrates agents. Agnostic to the use case.
- **Services built on ContextCore** - concrete implementations that consume the infrastructure for a specific purpose.

Examples of services that could be built on top:
- Operational efficiency and process flow control for enterprise environments
- Proactive coding assistance for individual developers
- Adaptive learning environments
- Any other context-aware service anyone chooses to build

This is the same distinction as Internet vs. web applications, Linux vs. enterprise operating systems, or Ethereum vs. decentralized applications. ContextCore is the layer underneath.

---

## The Problem

Ambient agents today are built for enterprise infrastructure: monitoring servers, pipelines, and cloud systems. The problem at the **individual user level** remains unsolved. No system exists that understands how *you* work, learns *your* specific patterns, and connects the right AI tool at the right moment — without interrupting your flow or asking you anything.

And no open infrastructure exists that allows anyone to build that kind of context-aware service without starting from scratch.

---

## What ContextCore Provides

ContextCore runs silently in the background. It observes user activity across all applications and devices, classifies it into behavioral contexts, and routes to the appropriate specialized agent automatically.

It does not respond to commands. It understands situations.

---

## Architecture

```
[Windows / macOS / Linux / Browser]
              ↓
 [Platform-specific signal adapters]
              ↓
      [Signal normalizer]
              ↓
   [Temporal filtering engine]
    confidence scoring + time window
              ↓
   [Adaptive context classifier]
    self-defined modes + learning
              ↓
     [Adaptive learning engine]
    pattern confirmation + confidence
              ↓
  [Synchronized user profile - DID W3C]
              ↓
    [Agent orchestration layer]
     OpenCode + custom agents
              ↓
       [Blockchain layer]
    identity + hashes + permissions + tokens
```

---

## Core Components

### A1 - Normalized Signal

Each platform adapter captures raw OS events and normalizes them into a common format. The AI generates a brief description of what just happened.

```json
{
  "action": "window-change",
  "type": "navigation",
  "timestamp": "2026-05-01T10:32:00Z",
  "description": "User switched to VSCode after browsing GitHub"
}
```

### A2 - Context Classifier

Receives a continuous stream of normalized signals and groups them into behavioral patterns using a temporal filtering window. Scores context candidates before committing. Does not react to isolated actions - it reads causal chains.

```json
{
  "pattern_id": "ptn_unique_id",
  "sequence": ["window-change", "file-open", "keystroke-burst"],
  "confidence": null,
  "derived_from": ["ptn_previous_id"],
  "occurrences": 0
}
```

`confidence` starts as `null`. The learning engine assigns it based on observed evidence. Until a threshold is reached, the pattern exists but does not trigger any agent.

### A3 - Adaptive Learning Engine

Observes confirmed patterns over time and decides whether they are real or noise. Uses temporal data to evaluate frequency, duration, and consistency.

```json
{
  "pattern_id": "ptn_unique_id",
  "action_id": "act_unique_id",
  "datetime_start": "2026-05-01T10:32:00Z",
  "datetime_end": "2026-05-01T12:15:00Z"
}
```

Derived auxiliary queries: duration, frequency, time-of-day distribution, behavioral consistency. ContextCore does not use a fixed list of contexts - it **discovers and names them autonomously** based on each user's recurring patterns.

### A4 - User Profile

Each user is identified by a **W3C Decentralized Identifier (DID)**, independent of any central server or identity provider. The profile is portable across devices by design.

```json
{
  "did": "did:example:123abc",
  "created_at": "2026-05-01T00:00:00Z",
  "devices": ["device_id_1", "device_id_2"],
  "contexts": ["ptn_id_1", "ptn_id_2"],
  "profile_hash": "verifiable_hash_on_chain"
}
```

### A5 - Agent Orchestrator

Receives confirmed context and routes to the appropriate specialized agent. The pattern-to-agent mapping is configurable and extensible. The orchestration logic does not change as new agents are added.

```json
{
  "pattern_id": "ptn_unique_id",
  "confidence": 0.78,
  "sequence": ["window-change", "file-open", "keystroke-burst"],
  "agent": "opencode",
  "action": "suggest",
  "parameters": {
    "context": "coding-session",
    "mode": "proactive"
  }
}
```

---

## Blockchain Layer

The blockchain is a **transversal infrastructure layer active from module one**, not a future feature.

> The blockchain does not contain the context. It contains the proof that the context exists, belongs to the user, and has not been tampered with.

### On-chain (public, verifiable, non-sensitive)
- Decentralized user identity (DID W3C)
- Authorized device registry
- Permissions between user, devices, and agents
- Integrity hashes of encrypted contextual data
- Profile version and snapshot registry
- Access revocation
- Tokens and access credentials
- Economic model / tokenization

### Off-chain (private, encrypted, user-owned)
- Behavioral events
- Activity history
- Contextual profile
- Embeddings
- Preferences
- Relationships between projects, files, apps, and agents
- Adaptive memory
- Pattern usage logs

All off-chain data is: **encrypted, signed, versioned, cross-device syncable, and verifiable via on-chain hashes.**

---

## Design Principles

**Infrastructure over product.** ContextCore is a platform others build on. Use cases are external implementations, not core features.

**Abstracted dependencies.** The core logic does not depend on any specific platform, AI model, or agent. Each is a replaceable implementation behind a common interface.

**Context over commands.** The system acts based on what the user is doing, not what they ask. No commands - only detected situations.

**Privacy first.** All signal processing happens locally. The user profile is owned entirely by the user via DID. No sensitive data leaves the device unencrypted.

**Composable agents.** Any specialized agent plugs in by mapping a pattern to an action. The architecture does not change as it scales.

**Native blockchain from day one.** Each active module writes confirmed patterns to the blockchain from the start. Data accumulates while the project grows, enabling distributed federated learning when advanced stages are reached.

---

## Project Phases

```
Phase A - Architecture design        [done]
  A1  Normalized signal
  A2  Context classifier
  A3  Adaptive learning engine
  A4  User profile with DID W3C
  A5  Agent orchestrator

Phase B - Local validation
  B1  Database schema
  B2  Simulated data
  B3  Functional output validation per layer

Phase C - Blockchain integration
  C1  DID identity implementation
  C2  On-chain registry
  C3  Off-chain encrypted storage
  C4  Cross-device sync
  C5  Tokenization model
```

---

## Repository Structure

```
/agent-core          - classifier, temporal filter, learning engine
/adapters
   /windows          - Win32 API, UI Automation
   /macos            - Accessibility API
   /linux            - X11 / Wayland
   /browser          - Extension with active tab permissions
/user-profile        - local storage + cross-device sync via DID
/integrations
   /opencode         - coding context agent
   /custom           - extensible agent interface
/docs
```

---

## Status

Architecture design phase complete. Moving to local validation.
Contributions welcome - especially platform adapter implementations.

---

## Related Concepts

Ambient Agents - Context-aware computing - Agentic AI orchestration - Adaptive user modeling - Decentralized identity - Federated learning

---

## License

MIT
