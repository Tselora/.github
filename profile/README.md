# Tselora

Tselora is an open-source project for making AI agent execution **observable, structured, and understandable**.

It records what an existing agent actually did as a stream of structured events, then stores that stream as an authoritative log. It is not an agent framework or orchestrator. It is meant to sit beside agents you already run.

Source: [github.com/Tselora/Tselora](https://github.com/Tselora/Tselora)

## Current status

Tselora is in **early development**. Work is incremental. Several documented components (projections, UI, replay, runtime control, framework adapters) are **not implemented yet**.

The first working slice is:

```text
Python function
    → Tselora SDK decorator
    → AgentEvent
    → HTTP transport
    → FastAPI collector
    → JSONL event store
```

That slice shows that a normal Python function can emit a Tselora event, and that the collector can persist it to the JSONL event log (the current source of truth).

## Architecture principles

These are the rules the project is being built on. They describe how the system is designed, not a list of finished products.

- Event-driven model with an explicit, framework-neutral event protocol
- Causal links via `parent_event_id` (not “whatever arrived next”)
- Event IDs and per-run sequence numbers assigned by the SDK at emit time
- Collector owns persistence; the SDK does not write the log directly
- JSONL files as the initial authoritative store (local, file-based)
- No extra infrastructure (databases, brokers, clouds) in this stage
- Small, reviewable steps rather than a large unfinished platform

## Future work

Not available today. Possible later directions:

- Event projection (graph, timeline, run/node state)
- Richer execution visualization
- Runtime controls
- Replay / time-travel of recorded runs
- Framework adapters
- Other persistence backends
- Additional agent and runtime integrations

## Open source

Tselora is developed in the open so the execution model stays simple enough to read, test, and reason about. The goal is a clear foundation for observing AI-agent runs—not a closed control plane.

The implementation repository uses the Apache License 2.0 (see [LICENSE](https://github.com/Tselora/Tselora/blob/main/LICENSE) in the source repo).
