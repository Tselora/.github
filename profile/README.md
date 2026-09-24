# Tselora

Tselora makes AI agent execution **observable, structured, and understandable**.

It records what an existing agent actually did as a stream of structured events, then stores that stream as an authoritative log. It is not an agent framework or orchestrator. It sits beside agents you already run.

Install: `pip install tselora` (Python 3.12+)

Usage examples and the demo GIF: [github.com/Tselora/Tselora](https://github.com/Tselora/Tselora)

The implementation source is currently private.

## What it does

- Framework-neutral event protocol: agent actions become structured `AgentEvent`s
- Causal links via `parent_event_id`, per-run sequence numbers, logical node IDs with execution instances (`Researcher` becomes `Researcher#1`)
- FastAPI collector with an append-only JSONL event store
- Canonical projection into graph, timeline, and run/node state, with replay and time-travel
- Live WebSocket patches for dashboards, plus a web Explorer UI
- Adapters for OpenTelemetry, LangGraph, the OpenAI Agents SDK, and CrewAI

## Status

Actively developed. Shipped: core SDK, collector (REST + WebSocket), Explorer UI, replay, and framework adapters. Work continues incrementally.

## Architecture principles

- Event-driven model with an explicit, framework-neutral event protocol
- Causal links via `parent_event_id` (not "whatever arrived next")
- Event IDs and per-run sequence numbers assigned by the SDK at emit time
- Collector owns persistence; the SDK does not write the log directly
- Append-only event log as the authoritative store
- Small, reviewable steps rather than a large unfinished platform

## License

The implementation uses the Apache License 2.0.
