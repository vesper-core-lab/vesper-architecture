# Vesper Object System

The Object System is one of the core design directions of Vesper.

Vesper does not treat business operations as plain text conversations only.

Instead, it organizes work around structured business objects.

## Why Objects Matter

In real organizations, work is not only a sequence of messages.

Work usually happens around persistent entities such as:

- People
- Products
- Campaigns
- Orders
- Reports
- Tasks
- Files
- Events
- Decisions

The Object System allows Vesper to connect conversations, tasks, workflows, and reports to structured operational entities.

## Current Public Object Direction

The first public object direction is based on MCN and cross-border e-commerce operations.

Example objects may include:

- Creator
- Product
- Campaign
- Video
- Order
- Report
- Task

These objects are useful because they represent real operational units in business workflows.

## Example Object Relationship

```text
Creator
→ participates in Campaign

Product
→ belongs to Campaign

Campaign
→ generates Videos, Orders, Reports, and Tasks

Task
→ may be linked to Creator, Product, Campaign, Video, Order, or Report
```

## Object System v2 Direction

The next object system direction includes:

- Better object persistence
- Consistent create and list behavior
- More object types
- Task-object relationships
- Object command normalization
- Duplicate task prevention
- Enhanced reporting

## Governance Boundary

Business objects should not randomly modify the core system.

They should attach to the Vesper core through clear schemas, controlled workflows, and governed execution paths.

## Design Goal

The Object System should help Vesper move from simple message response to structured operational intelligence.
