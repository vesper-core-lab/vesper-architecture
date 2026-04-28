# Vesper Architecture

Vesper is designed around a layered architecture.

```text
Input Adapters
→ Unified Event Layer
→ Planner Engine / Task Graph
→ Approval Engine
→ Guardrail / Governor
→ Execution Skills
→ Feedback Memory
```

## 1. Input Adapters

Input adapters receive signals from different perception channels.

Examples may include:

- Messaging platforms
- Voice
- Images
- Video
- Business systems
- Human commands
- External APIs

The input channel should not define the whole system.

Telegram, for example, can be one input adapter, but it should not become the architecture itself.

## 2. Unified Event Layer

The event layer converts inputs and system actions into structured facts.

Events should describe what has happened.

They should not be treated as uncontrolled future intent.

## 3. Planner Engine / Task Graph

The planner converts user goals, object states, and operational context into task structures.

The task graph should help the system understand dependencies, priorities, and execution order.

## 4. Approval Engine

The approval layer allows human arbitration before high-impact actions.

This is important for enterprise use cases where uncontrolled autonomy can create operational risk.

## 5. Guardrail / Governor

The governor controls what the system is allowed to do.

It should protect the core trunk, prevent unsafe execution, and keep business modules from polluting the core system.

## 6. Execution Skills

Skills are controlled execution units.

They may support actions such as:

- Creating tasks
- Generating reports
- Calling APIs
- Updating objects
- Producing structured outputs

## 7. Feedback Memory

Feedback memory stores lessons from previous operations.

The system should gradually learn from human corrections, approvals, failures, and successful workflows.

## Design Principle

The core system should remain stable.

Industry modules should evolve outside the core through clear boundaries.
