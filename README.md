# ContextCore

> Decentralized contextual intelligence infrastructure.

An open source adaptive ambient agent that observes user behavior in real time, autonomously discovers behavioral contexts, and orchestrates specialized AI agents across all devices — without requiring any manual command.

---

## The Problem

Ambient agents today are built for enterprise infrastructure: monitoring servers, pipelines, and cloud systems. The problem at the **individual user level** remains unsolved. No system exists that understands how *you* work, learns *your* specific patterns, and connects the right AI tool at the right moment — without interrupting your flow or asking you anything.

---

## What ContextCore Does

ContextCore runs silently in the background on your desktop. It observes what you are doing across all your applications and devices, classifies your activity into behavioral contexts, and routes to the right specialized agent automatically.

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
    identity + hashes + permissions
```

---

## Core Components

### A1 - Normalized Signal

Each platform adapter captures raw OS events and normalizes them into a common format before passing them to the classifier. The AI generates a brief description of what just happened.

```json
{
  "action": "window-change",
  "type": "navigation",
  "timestamp": "2026-05-01T10:32:00Z",
  "description": "User switched to VSCode after browsing GitHub"
}
```

### A2 - Context Classifier

Receives a continuous stream of normalized signals and groups them into behavioral patterns using a temporal filtering window. Rather than reacting to a single action, it scores context candidates before committing.

```json
{
  "pattern_id": "ptn_unique_id",
  "sequence": ["window-change", "file-open", "keystroke-burst"],
  "confidence": null,
  "derived_from": ["ptn_previous_id"],
  "occurrences": 0
}
```

`confidence` starts as `null`. The learning engine assigns it based on observed evidence. Until a confidence threshold is reached, the pattern exists but does not trigger any agent.

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

From these four fields, auxiliary queries derive: duration, frequency, time-of-day distribution, and behavioral consistency. The engine assigns confidence based on this evidence.

ContextCore does not use a fixed list of contexts. It **discovers and names them autonomously** based on recurring patterns in each user's behavior.

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

Receives confirmed context from the classifier and routes to the appropriate specialized agent. The mapping between patterns and agents is configurable and extensible.

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

Any specialized agent can be added by mapping a pattern to an action. The orchestration logic does not change.

---

## Blockchain Layer

ContextCore uses blockchain as a **transversal infrastructure layer active from module one**, not as a future feature. The principle is simple:

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

**Abstracted dependencies.** The core logic does not depend on any specific platform, AI model, or agent. Each is a replaceable implementation behind a common interface.

**Context over commands.** The agent acts based on what the user is doing, not what they ask it to do.

**Privacy first.** All signal processing happens locally. The user profile is owned entirely by the user via DID.

**Composable agents.** ContextCore is an orchestration layer. Any specialized agent plugs in as a target for a detected context.

**Native blockchain from day one.** Each active module writes confirmed patterns to the blockchain. Data accumulates while the project grows, enabling federated distributed learning when advanced learning stages are reached.

---

## Project Phases

```
Phase A - Architecture design        [in progress]
  A1  Normalized signal              [done]
  A2  Context classifier             [done]
  A3  Adaptive learning engine       [done]
  A4  User profile with DID W3C      [done]
  A5  Agent orchestrator             [done]

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

Architecture design phase. Contributions welcome, especially platform adapter implementations.

---

## Related Concepts

Ambient Agents - Context-aware computing - Agentic AI orchestration - Adaptive user modeling - Decentralized identity - Federated learning

---

## License

MIT
