# Vesper Architecture

Vesper is an experimental AI Agent Operating System designed for governed workflows, object-based operations, and industry-specific modules.

This repository contains public architecture notes, design principles, non-sensitive examples, and development logs.

The core implementation is currently private while the system is under active prototyping.

## Public Demo Gallery

Vesper is currently publishing synthetic, non-sensitive demos to show how its object-based workflow model may work in real operational scenarios.

These demos do not include real customer data, real partner information, internal screenshots, raw interviews, production configurations, server paths, or confidential business workflows.

### MCN LiveOps Demos

- [Livestream Session Demo](examples/mcn-demo/02-livestream-session-demo.md)

  Shows how Vesper may transform a single livestream record into structured objects, stream metrics, feedback records, follow-up tasks, and a simple report.

- [Weekly LiveOps Report Demo](examples/mcn-demo/03-weekly-liveops-report-demo.md)

  Shows how Vesper may summarize multiple livestream sessions into a weekly operational report, detect data quality issues, generate feedback records, create follow-up tasks, and surface operational risks.

- [Product to Campaign Workflow Demo](examples/mcn-demo/04-product-to-campaign-workflow-demo.md)

  Shows how Vesper may connect a product, campaign, creator task, livestream session, performance metrics, feedback, report, and follow-up task into a structured workflow.

### Public Demo Direction

The public demo gallery is designed to show Vesper's direction without exposing private implementation details.

Current demo focus:

- Object-based operations
- Livestream session modeling
- Stream metric abstraction
- Product-to-campaign workflow connection
- Data quality checks
- Feedback records
- Follow-up tasks
- Weekly reporting
- Operational memory direction

The goal is to demonstrate that Vesper is not a simple chatbot.

Vesper is designed to help structure operational workflows around people, objects, events, reports, decisions, and tasks.

## Repository Map

This repository is organized as follows:

- [Vision](docs/01-vision.md)
- [Architecture](docs/02-architecture.md)
- [Governance-First Design](docs/03-governance-first.md)
- [Public Roadmap](docs/04-roadmap.md)
- [Object System](docs/05-object-system.md)
- [Public Boundary](docs/06-public-boundary.md)
- [MCN Module Public Note](docs/07-mcn-module-public-note.md)
- [First Build Log](build-log/2026-04-28-github-init.md)
- [MCN Demo Examples](examples/mcn-demo)

## Current Public Materials

The current public materials include:

- High-level Vesper vision
- Layered architecture direction
- Governance-first design principles
- Public roadmap
- Object System explanation
- Synthetic MCN object examples
- Build log for public documentation setup

## What is Vesper?

Vesper is not designed as a simple chatbot.

It is designed as an AI Agent Operating System that coordinates:

```text
Input Adapters
→ Unified Event Layer
→ Planner Engine / Task Graph
→ Approval Engine
→ Guardrail / Governor
→ Execution Skills
→ Feedback Memory
```

The goal is to help organizations operate with structured AI workflows, traceable decisions, modular industry objects, and governed execution.

## Why Governance Matters

Most AI agents focus on autonomy.

Vesper focuses first on governance.

The system should not randomly modify its core logic or execute actions without structure.

Instead, it should evolve through:

- Controlled extensions
- Traceable events
- Approval layers
- Modular business capabilities

## Core Principles

- Events represent facts, not future intent.
- Business modules should not pollute the core trunk.
- New capabilities should be added through controlled extension.
- Human approval should remain available for high-impact decisions.
- The system should accumulate operational memory over time.

## Current Public Scope

This public repository may include:

- Architecture notes
- Design principles
- Public roadmap
- Non-sensitive object examples
- Build logs
- Conceptual diagrams
- Industry module sketches

This repository will not include:

- Private implementation code
- Production configuration
- API keys or tokens
- Customer data
- Internal business documents
- Raw interview records
- Commercially sensitive workflows
