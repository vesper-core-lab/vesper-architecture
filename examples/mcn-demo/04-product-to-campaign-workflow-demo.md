# Product to Campaign Workflow Demo

This is a synthetic, non-sensitive demo for Vesper's MCN LiveOps module.

It shows how Vesper may connect a product, campaign, creator task, livestream session, performance metrics, feedback, and report into a structured workflow.

This demo does not include real customer data, real partner information, internal screenshots, raw interviews, production configuration, server paths, or confidential business workflows.

## Scenario

A MCN operations team wants to promote a product through a livestream campaign.

The team needs to:

- Register the product
- Create a campaign
- Assign a host / creator
- Create a livestream task
- Record livestream performance
- Generate feedback
- Produce a campaign report
- Create follow-up tasks

The goal is to show how Vesper may move from isolated records to a connected operational workflow.

## Synthetic Input

A user may tell Vesper:

```text
Create a campaign for a demo product.

Product:
Name: Demo Health Supplement
Category: health
Target Account: demo_health_account

Campaign:
Name: April Health Livestream Test
Period: 2026-04-15 to 2026-04-19
Goal: Test livestream conversion potential

Creator:
Host: Creator A
Assistant: Operator B

Livestream:
Date: 2026-04-15
Duration: 2.0 hours
GMV: 1200.00
Items Sold: 38
Data Quality: valid
```

## Expected Vesper Interpretation

Vesper should identify several connected objects:

- Product
- Campaign
- Account
- Creator / Host
- Assistant / Operator
- Task
- LiveSession
- StreamMetric
- FeedbackRecord
- CampaignReport

## Object 1: Product

```json
{
  "object_type": "product",
  "product_id": "PROD-demo-health-supplement",
  "name": "Demo Health Supplement",
  "category": "health",
  "status": "active",
  "notes": "Synthetic product for public demo."
}
```

## Object 2: Account

```json
{
  "object_type": "account",
  "account_id": "ACC-demo-health",
  "account_name": "demo_health_account",
  "platform": "demo_platform",
  "category": "health",
  "status": "active"
}
```

## Object 3: Campaign

```json
{
  "object_type": "campaign",
  "campaign_id": "CAMPAIGN-202604-health-test",
  "name": "April Health Livestream Test",
  "period_start": "2026-04-15",
  "period_end": "2026-04-19",
  "goal": "Test livestream conversion potential",
  "linked_product_ids": [
    "PROD-demo-health-supplement"
  ],
  "linked_account_ids": [
    "ACC-demo-health"
  ],
  "status": "active"
}
```

## Object 4: Creator / Host

```json
{
  "object_type": "creator",
  "creator_id": "CREATOR-A",
  "name": "Creator A",
  "role": "host",
  "status": "active",
  "linked_accounts": [
    "ACC-demo-health"
  ]
}
```

## Object 5: Assistant / Operator

```json
{
  "object_type": "operator",
  "operator_id": "OPERATOR-B",
  "name": "Operator B",
  "role": "assistant",
  "status": "active"
}
```

## Object 6: Campaign Task

```json
{
  "object_type": "task",
  "task_id": "TASK-CAMPAIGN-202604-health-test-001",
  "title": "Run livestream test for Demo Health Supplement",
  "linked_object_type": "campaign",
  "linked_object_id": "CAMPAIGN-202604-health-test",
  "assigned_to": "CREATOR-A",
  "support_role": "OPERATOR-B",
  "priority": "medium",
  "status": "pending",
  "reason": "Test livestream conversion potential for the demo product."
}
```

## Object 7: LiveSession

```json
{
  "object_type": "live_session",
  "live_session_id": "LS-20260415-demo-health",
  "date": "2026-04-15",
  "campaign_id": "CAMPAIGN-202604-health-test",
  "product_ids": [
    "PROD-demo-health-supplement"
  ],
  "account_id": "ACC-demo-health",
  "host_id": "CREATOR-A",
  "assistant_id": "OPERATOR-B",
  "duration_hours": 2.0,
  "status": "completed",
  "data_quality": "valid"
}
```

## Object 8: StreamMetric

```json
{
  "object_type": "stream_metric",
  "metric_id": "METRIC-LS-20260415-demo-health",
  "live_session_id": "LS-20260415-demo-health",
  "campaign_id": "CAMPAIGN-202604-health-test",
  "product_id": "PROD-demo-health-supplement",
  "total_gmv": 1200.00,
  "items_sold": 38,
  "stream_hours": 2.0,
  "gmv_per_hour": 600.00,
  "items_sold_per_hour": 19,
  "data_quality": "valid"
}
```

## Workflow Linkage

Vesper should connect the workflow like this:

```text
Product
→ Campaign
→ Campaign Task
→ Creator / Host
→ LiveSession
→ StreamMetric
→ FeedbackRecord
→ CampaignReport
→ Follow-up Task
```

The important idea is that each object should not exist alone.

Each object should be connected to the workflow.

## Example Operational Check

Vesper may run simple checks.

```json
{
  "check_result": "passed",
  "linked_objects": {
    "product": true,
    "campaign": true,
    "account": true,
    "creator": true,
    "assistant": true,
    "live_session": true,
    "stream_metric": true
  },
  "missing_fields": [],
  "data_quality": "valid"
}
```

## Example FeedbackRecord

```json
{
  "object_type": "feedback_record",
  "feedback_id": "FB-CAMPAIGN-202604-health-test-001",
  "linked_campaign_id": "CAMPAIGN-202604-health-test",
  "linked_session_id": "LS-20260415-demo-health",
  "issue": "baseline_created",
  "observation": "The first livestream session created a baseline for GMV per hour and items sold per hour.",
  "suggested_action": "Compare future sessions against this baseline and track whether the product shows stable conversion potential.",
  "status": "open"
}
```

## Example Campaign Report

Vesper may generate a simple campaign report.

```markdown
# Campaign Report

Campaign: April Health Livestream Test  
Product: Demo Health Supplement  
Period: 2026-04-15 to 2026-04-19  

## Summary

One livestream session was completed for the campaign.

## Linked Objects

- Product: Demo Health Supplement
- Account: demo_health_account
- Host: Creator A
- Assistant: Operator B
- LiveSession: LS-20260415-demo-health

## Performance

- Duration: 2.0 hours
- GMV: 1200.00
- Items Sold: 38
- GMV per Hour: 600.00
- Items Sold per Hour: 19
- Data Quality: valid

## Operational Notes

This session can be used as the first campaign baseline.

Future sessions should be compared against this baseline.

## Suggested Actions

- Continue tracking campaign performance.
- Compare future hosts and session formats.
- Review whether this product has stable conversion potential.
- Create follow-up tasks if performance drops below baseline.
```

## Example Follow-up Task

```json
{
  "object_type": "task",
  "task_id": "TASK-CAMPAIGN-202604-health-test-REVIEW",
  "title": "Review campaign baseline for Demo Health Supplement",
  "linked_object_type": "campaign",
  "linked_object_id": "CAMPAIGN-202604-health-test",
  "priority": "medium",
  "status": "pending",
  "reason": "The first livestream session created a baseline that should be compared with future sessions."
}
```

## Missing Link Example

If a livestream session is recorded without a linked campaign or product, Vesper should detect the issue.

Example incomplete input:

```text
Record livestream session.

Date: 2026-04-18
Account: demo_health_account
Host: Creator A
Assistant: Operator B
Duration: 2.0 hours
GMV: 900.00
Items Sold: 22
Product:
Campaign:
```

Expected system signal:

```json
{
  "check_result": "needs_review",
  "missing_links": [
    "product_id",
    "campaign_id"
  ],
  "recommended_action": "Create a task to link the livestream session to a product and campaign."
}
```

Example task:

```json
{
  "object_type": "task",
  "task_id": "TASK-LINK-LS-20260418-demo-health",
  "title": "Link livestream session to product and campaign",
  "linked_object_type": "live_session",
  "linked_object_id": "LS-20260418-demo-health",
  "priority": "high",
  "status": "pending",
  "reason": "The livestream session is missing product and campaign links."
}
```

## Why This Demo Matters

This demo shows how Vesper may connect business objects into a workflow.

A simple chatbot may summarize a campaign.

Vesper should eventually help structure the operation itself.

It should help answer:

- Which product is being promoted?
- Which campaign does the livestream belong to?
- Which creator is responsible?
- Which assistant supported the session?
- What metrics were recorded?
- What feedback was generated?
- What follow-up tasks should be created?
- What should be remembered for future operations?

The goal is to move from scattered campaign notes to connected operational intelligence.

## Public Boundary

This demo is public and synthetic.

It does not include:

- Real customer data
- Real partner information
- Internal screenshots
- Raw interview records
- Private business plans
- Production configuration
- API keys or tokens
- Server paths
- Confidential implementation details

## Status

This is an early public demo.

The private implementation may evolve separately as Vesper continues to develop its MCN module, object system, workflow engine, approval layer, and reporting structure.
