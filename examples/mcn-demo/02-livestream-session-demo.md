# Livestream Session Demo

This is a synthetic, non-sensitive demo for Vesper's MCN LiveOps module.

It shows how a livestream operation record may be transformed into structured objects, metrics, feedback, follow-up tasks, and a simple report.

This demo does not include real customer data, real partner information, internal screenshots, raw interviews, production configuration, server paths, or confidential business workflows.

## Scenario

A MCN operations team runs a livestream session for a demo account.

The team wants to record the session, track performance, identify issues, create follow-up tasks, and generate a simple operational report.

## Synthetic Input

A user may tell Vesper:

```text
Record a livestream session.

Date: 2026-04-15
Account: demo_health_account
Host: Creator A
Assistant: Operator B
Start Time: 2026-04-15 15:00 EDT
End Time: 2026-04-15 17:00 EDT
Duration: 2.0 hours
GMV: 1200.00
Items Sold: 38
Data Quality: valid
```

## Expected Vesper Interpretation

Vesper should identify that this input contains several operational objects:

- Account
- Creator / Host
- Assistant / Operator
- LiveSession
- StreamMetric
- FeedbackRecord
- Report
- Task

## Object 1: Account

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

## Object 2: Creator / Host

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

## Object 3: Assistant / Operator

```json
{
  "object_type": "operator",
  "operator_id": "OPERATOR-B",
  "name": "Operator B",
  "role": "assistant",
  "status": "active"
}
```

## Object 4: LiveSession

```json
{
  "object_type": "live_session",
  "live_session_id": "LS-20260415-demo-health",
  "date": "2026-04-15",
  "account_id": "ACC-demo-health",
  "host_id": "CREATOR-A",
  "assistant_id": "OPERATOR-B",
  "start_time": "2026-04-15T15:00:00-04:00",
  "end_time": "2026-04-15T17:00:00-04:00",
  "duration_hours": 2.0,
  "status": "completed",
  "data_quality": "valid"
}
```

## Object 5: StreamMetric

```json
{
  "object_type": "stream_metric",
  "metric_id": "METRIC-LS-20260415-demo-health",
  "live_session_id": "LS-20260415-demo-health",
  "total_gmv": 1200.00,
  "items_sold": 38,
  "stream_hours": 2.0,
  "gmv_per_hour": 600.00,
  "items_sold_per_hour": 19,
  "data_quality": "valid",
  "source": "synthetic_manual_entry"
}
```

## Operational Check

Vesper may run simple public demo checks.

Example checks:

- Is start time present?
- Is end time present?
- Is duration present?
- Is GMV present?
- Are items sold present?
- Is the session linked to an account?
- Is the session linked to a host?
- Is the session linked to an assistant?
- Is data quality valid?

For this synthetic demo:

```json
{
  "check_result": "passed",
  "missing_fields": [],
  "data_quality": "valid"
}
```

## Example FeedbackRecord

If the session is valid but performance needs review, Vesper may create a feedback record.

```json
{
  "object_type": "feedback_record",
  "feedback_id": "FB-LS-20260415-demo-health",
  "live_session_id": "LS-20260415-demo-health",
  "issue": "performance_review",
  "observation": "The livestream session has valid data. GMV per hour and items sold per hour can be reviewed against future baselines.",
  "suggested_action": "Compare this session with future sessions from the same account and host.",
  "status": "open"
}
```

## Example Follow-up Task

Vesper may create a follow-up task for operational review.

```json
{
  "object_type": "task",
  "task_id": "TASK-REVIEW-LS-20260415-demo-health",
  "title": "Review livestream performance for demo_health_account on 2026-04-15",
  "linked_object_type": "live_session",
  "linked_object_id": "LS-20260415-demo-health",
  "priority": "medium",
  "status": "pending",
  "reason": "Create baseline review for livestream performance."
}
```

## Example Report

Vesper may generate a simple report.

```markdown
# MCN LiveOps Report

Period: 2026-04-15

## Summary

One livestream session was recorded for demo_health_account.

## Session

- Account: demo_health_account
- Host: Creator A
- Assistant: Operator B
- Duration: 2.0 hours
- GMV: 1200.00
- Items Sold: 38
- GMV per Hour: 600.00
- Items Sold per Hour: 19
- Data Quality: valid

## Operational Notes

The session data is complete.

This session can be used as an early baseline for future comparison.

## Suggested Actions

- Compare this session with future sessions.
- Track host stability over multiple sessions.
- Track assistant data recording quality.
- Use repeated feedback records to improve SOPs.
```

## Missing Data Example

If a future livestream record is incomplete, Vesper should mark it as needing review.

Example input:

```text
Record livestream session.

Date: 2026-04-16
Account: demo_home_account
Host: Creator B
Assistant: Operator B
Start Time: 2026-04-16 12:00 EDT
End Time:
Duration:
GMV: 0
Items Sold: 0
```

Expected system signal:

```json
{
  "live_session_id": "LS-20260416-demo-home",
  "data_quality": "missing",
  "missing_fields": [
    "end_time",
    "duration_hours"
  ],
  "recommended_action": "Create a data completion task."
}
```

Example task:

```json
{
  "object_type": "task",
  "task_id": "TASK-DATA-CHECK-LS-20260416-demo-home",
  "title": "Complete missing livestream data for demo_home_account on 2026-04-16",
  "linked_object_type": "live_session",
  "linked_object_id": "LS-20260416-demo-home",
  "priority": "high",
  "status": "pending",
  "reason": "End time and duration are missing."
}
```

## Why This Demo Matters

This demo shows how Vesper may move from plain text input to structured operational intelligence.

A simple chatbot may summarize the livestream record.

Vesper should eventually help structure the operation:

- Identify objects
- Link people to sessions
- Record performance metrics
- Detect missing data
- Generate feedback records
- Create follow-up tasks
- Produce reports
- Accumulate operational memory

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
