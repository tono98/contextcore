# ContextCore

> An open source adaptive ambient agent that detects user context in real time and orchestrates specialized AI agents across devices.

---

## What is ContextCore?

ContextCore is a cross-platform background agent that observes user activity signals in real time, classifies them into behavioral contexts, and routes to specialized AI agents based on what the user is doing — without requiring any manual command.

Unlike traditional AI assistants that wait to be invoked, ContextCore is **proactive, context-aware, and adaptive**. It learns from the user's behavior over time, autodiscovers their personal working modes, and synchronizes a user profile across all devices.

---

## The Problem

Ambient agents today are built for enterprise infrastructure: monitoring servers, pipelines, and systems. No one has solved the problem at the **individual user level** — a desktop agent that understands *you*, learns *your* patterns, and connects the right AI tool at the right moment without interrupting your flow.

---

## How It Works

```
[Windows / macOS / Linux / Browser]
           ↓
[Platform-specific signal adapters]
           ↓
     [Signal normalizer]
           ↓
  [Temporal filtering engine]
   (confidence scoring + window)
           ↓
  [Adaptive context classifier]
   (self-defined modes + learning)
           ↓
    [Synchronized user profile]
           ↓
 [Agent orchestration layer]
  (OpenCode, custom agents, etc.)
```

### Signal capture (per platform)
- Active application
- Browser URL
- Open files
- Keyboard input patterns
- Mouse activity

### Temporal filtering
Rather than reacting to a single action, ContextCore observes a time window and scores context candidates before committing:

```
detected signals
      ↓
[time window observation]
      ↓
context candidates with confidence score
  e.g. coding 78% / research 15% / other 7%
      ↓
threshold reached? → name it, study it, store it
not reached?       → keep observing
```

### Context model (user profile)
Each confirmed context is stored as:

```json
{
  "id": "ctx_unique_id",
  "name": "deep-coding-session",
  "category": "development",
  "actions": {
    "types": ["keystroke", "file-edit", "terminal-command"],
    "count": 142,
    "interval_seconds": 1800
  }
}
```

### Adaptive learning
ContextCore does not use a fixed list of contexts. It **discovers and names them** based on recurring patterns in the user's behavior. Over time it learns:
- What signals trigger each context
- How long each context lasts
- When it typically occurs during the day
- How it relates to other contexts

---

## Architecture

```
/agent-core          ← classifier, temporal filter, learning engine
/adapters
   /windows          ← Win32 API, UI Automation
   /macos            ← Accessibility API
   /linux            ← X11 / Wayland
   /browser          ← Extension with active tab permissions
/user-profile        ← local storage + cross-device sync
/integrations
   /opencode         ← coding context agent
   /custom           ← extensible agent interface
/docs
```

Each platform adapter normalizes signals into a common format before passing them to the core. The classifier does not know — and does not care — which platform the signals came from.

---

## Design Principles

**Abstracted dependencies.** The core logic does not depend on any specific platform, model, or agent. Each is a replaceable implementation behind a common interface.

**Context over commands.** The agent acts based on what the user is doing, not what they ask it to do.

**Privacy first.** All signal processing happens locally. The user profile is owned by the user.

**Composable agents.** ContextCore is an orchestration layer. Any specialized agent can be plugged in as a target for a detected context.

---

## Status

Early design phase. Contributions welcome — especially platform adapter implementations.

---

## Related concepts

- Ambient Agents
- Context-aware computing
- Agentic AI orchestration
- Adaptive user modeling

---

## License

MIT
