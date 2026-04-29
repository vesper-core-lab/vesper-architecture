# Assistant Data Quality Workflow Demo

This is a synthetic, non-sensitive demo for Vesper's MCN LiveOps module.

It shows how Vesper may connect assistant work, livestream data entry, missing fields, data quality checks, review tasks, SOP improvement, and operational memory.

This demo does not include real customer data, real partner information, internal screenshots, raw interviews, salary details, recruiting channels, production configuration, server paths, or confidential business workflows.

## Scenario

A MCN operations team depends on assistants and operators to record livestream information.

The team needs livestream records to be complete and reliable.

However, real operations may contain problems such as:

- Missing start time
- Missing end time
- Missing duration
- Missing GMV
- Missing items sold
- Incorrect account link
- Missing host link
- Missing product link
- Missing campaign link
- Delayed feedback
- Incomplete post-session review

The goal is to show how Vesper may help turn data recording quality into a structured workflow.

## Synthetic Input

A user may tell Vesper:

```text
Review livestream data quality.

Date: 2026-04-16
Account: demo_home_account
Host: Creator B
Assistant: Operator B
Start Time: 2026-04-16 11:57 EDT
End Time:
Duration:
GMV: 0
Items Sold: 0
Data Quality: missing
```

## Expected Vesper Interpretation

Vesper should identify that this record contains several connected objects:

- Account
- HostProfile
- AssistantProfile
- LiveSession
- StreamMetric
- DataQualityCheck
- FeedbackRecord
- Follow-up Task
- SOPItem
- OperationalMemory

## Object 1: Account

```json
{
  "object_type": "account",
  "account_id": "ACC-demo-home",
  "account_name": "demo_home_account",
  "platform": "demo_platform",
  "category": "home",
  "status": "active"
}
```

## Object 2: HostProfile

```json
{
  "object_type": "host_profile",
  "host_id": "HOST-CREATOR-B",
  "person_id": "PERSON-CREATOR-B",
  "name": "Creator B",
  "role": "host",
  "category_fit": [
    "home",
    "lifestyle"
  ],
  "training_stage": "live_session_support",
  "status": "active"
}
```

## Object 3: AssistantProfile

```json
{
  "object_type": "assistant_profile",
  "assistant_id": "ASSISTANT-OPERATOR-B",
  "person_id": "PERSON-OPERATOR-B",
  "name": "Operator B",
  "role_type": "live_assistant",
  "supported_accounts": [
    "ACC-demo-health",
    "ACC-demo-home"
  ],
  "training_stage": "basic_data_recording",
  "status": "active"
}
```

## Object 4: LiveSession

```json
{
  "object_type": "live_session",
  "live_session_id": "LS-20260416-demo-home",
  "date": "2026-04-16",
  "account_id": "ACC-demo-home",
  "host_id": "HOST-CREATOR-B",
  "assistant_id": "ASSISTANT-OPERATOR-B",
  "start_time": "2026-04-16T11:57:00-04:00",
  "end_time": null,
  "duration_hours": null,
  "status": "needs_review",
  "data_quality": "missing"
}
```

## Object 5: StreamMetric

```json
{
  "object_type": "stream_metric",
  "metric_id": "METRIC-LS-20260416-demo-home",
  "live_session_id": "LS-20260416-demo-home",
  "total_gmv": 0.00,
  "items_sold": 0,
  "stream_hours": null,
  "gmv_per_hour": null,
  "items_sold_per_hour": null,
  "data_quality": "missing",
  "source": "synthetic_manual_entry"
}
```

## Object 6: DataQualityCheck

```json
{
  "object_type": "data_quality_check",
  "check_id": "DQC-LS-20260416-demo-home",
  "linked_session_id": "LS-20260416-demo-home",
  "linked_assistant_id": "ASSISTANT-OPERATOR-B",
  "check_result": "failed",
  "missing_fields": [
    "end_time",
    "duration_hours"
  ],
  "suspicious_fields": [
    "total_gmv",
    "items_sold"
  ],
  "reason": "The session is missing end time and duration. GMV and items sold are both zero and should be verified.",
  "recommended_action": "Create a data completion task and review assistant data recording quality."
}
```

## Object 7: FeedbackRecord

```json
{
  "object_type": "feedback_record",
  "feedback_id": "FB-DATA-LS-20260416-demo-home",
  "linked_session_id": "LS-20260416-demo-home",
  "linked_assistant_id": "ASSISTANT-OPERATOR-B",
  "issue": "incomplete_livestream_data",
  "observation": "The livestream record is missing end time and duration. Performance data should also be verified.",
  "suggested_action": "Complete missing fields and review data recording SOP.",
  "status": "open"
}
```

## Object 8: Follow-up Task

```json
{
  "object_type": "task",
  "task_id": "TASK-DATA-COMPLETE-LS-20260416-demo-home",
  "title": "Complete missing livestream data for demo_home_account",
  "linked_object_type": "live_session",
  "linked_object_id": "LS-20260416-demo-home",
  "assigned_to": "ASSISTANT-OPERATOR-B",
  "priority": "high",
  "status": "pending",
  "reason": "The livestream session is missing end time and duration."
}
```

## Object 9: SOPItem

```json
{
  "object_type": "sop_item",
  "sop_id": "SOP-ASSISTANT-LIVESTREAM-DATA-RECORDING",
  "title": "Assistant livestream data recording checklist",
  "category": "assistant_data_quality",
  "description": "Checklist for recording start time, end time, duration, account, host, assistant, GMV, items sold, product link, campaign link, and post-session notes.",
  "linked_role": "assistant",
  "status": "draft",
  "version": "0.1"
}
```

## Object 10: OperationalMemory

```json
{
  "object_type": "operational_memory",
  "memory_id": "MEMORY-ASSISTANT-DATA-QUALITY",
  "memory_type": "data_quality_pattern",
  "linked_role": "assistant",
  "issue": "incomplete_livestream_data",
  "summary": "Livestream operations may require strict data recording checklists because missing time fields, GMV fields, or product links can reduce the reliability of weekly reports and performance reviews.",
  "recommended_use": "Use this memory when creating assistant training tasks, data quality checks, or SOP improvements.",
  "status": "active"
}
```

## Workflow Linkage

Vesper should connect the assistant data quality workflow like this:

```text
AssistantProfile
→ LiveSession
→ StreamMetric
→ DataQualityCheck
→ FeedbackRecord
→ Follow-up Task
→ SOPItem
→ OperationalMemory
```

The important idea is that missing data should not remain hidden.

Missing data should become reviewable work.

## Example Operational Check

Vesper may run simple checks.

```json
{
  "check_result": "failed",
  "severity": "high",
  "missing_fields": [
    "end_time",
    "duration_hours"
  ],
  "suspicious_fields": [
    "total_gmv",
    "items_sold"
  ],
  "recommended_actions": [
    "Create data completion task",
    "Review assistant recording workflow",
    "Check whether SOP needs improvement"
  ]
}
```

## Example Vesper Response

Vesper may respond:

```text
Data quality check completed.

Result:
Needs review

Linked session:
LS-20260416-demo-home

Missing fields:
- End time
- Duration

Suspicious fields:
- GMV is 0
- Items sold is 0

Created task:
Complete missing livestream data for demo_home_account

Suggested SOP update:
Review assistant livestream data recording checklist

This issue may become operational memory if similar missing data appears repeatedly.
```

## Repeated Issue Example

If incomplete data appears across multiple sessions, Vesper should detect a repeated pattern.

Example repeated data quality records:

```json
[
  {
    "check_id": "DQC-LS-20260416-demo-home",
    "issue": "missing_duration",
    "linked_assistant_id": "ASSISTANT-OPERATOR-B"
  },
  {
    "check_id": "DQC-LS-20260418-demo-health",
    "issue": "missing_duration",
    "linked_assistant_id": "ASSISTANT-OPERATOR-B"
  },
  {
    "check_id": "DQC-LS-20260419-demo-beauty",
    "issue": "missing_product_link",
    "linked_assistant_id": "ASSISTANT-OPERATOR-D"
  }
]
```

Expected system signal:

```json
{
  "check_result": "repeated_data_quality_issue_detected",
  "issues": [
    "missing_duration",
    "missing_product_link"
  ],
  "affected_assistants": [
    "ASSISTANT-OPERATOR-B",
    "ASSISTANT-OPERATOR-D"
  ],
  "recommended_action": "Create assistant data quality training task and improve data recording SOP."
}
```

## Example Assistant Training Task

```json
{
  "object_type": "training_task",
  "task_id": "TRAINING-ASSISTANT-DATA-QUALITY-001",
  "person_id": "PERSON-OPERATOR-B",
  "assistant_id": "ASSISTANT-OPERATOR-B",
  "title": "Complete livestream data recording checklist training",
  "reason": "Repeated missing duration fields were detected in livestream records.",
  "priority": "high",
  "status": "pending",
  "linked_sop_id": "SOP-ASSISTANT-LIVESTREAM-DATA-RECORDING"
}
```

## Example SOP Improvement Task

```json
{
  "object_type": "task",
  "task_id": "TASK-SOP-ASSISTANT-DATA-QUALITY",
  "title": "Improve assistant livestream data recording SOP",
  "linked_object_type": "sop_item",
  "linked_object_id": "SOP-ASSISTANT-LIVESTREAM-DATA-RECORDING",
  "priority": "high",
  "status": "pending",
  "reason": "Repeated missing livestream fields indicate that the assistant data recording workflow needs clearer checkpoints."
}
```

## Example Weekly Data Quality Review

Vesper may generate a weekly assistant data quality review.

```markdown
# Weekly Assistant Data Quality Review

Period: 2026-04-13 to 2026-04-19

## Summary

This week contains multiple livestream data quality issues.

Detected issues:

- Missing end time
- Missing duration
- Missing product link
- Zero GMV requiring verification
- Zero items sold requiring verification

## Affected Roles

- Assistant / Operator B
- Assistant / Operator D

## Key Risks

Incomplete livestream data may reduce the reliability of:

- Weekly LiveOps reports
- Campaign performance comparison
- Host performance review
- Product conversion analysis
- Labor and profit calculation

## Suggested Actions

- Complete missing livestream data.
- Review assistant data recording checklist.
- Create assistant data quality training task.
- Improve livestream data recording SOP.
- Add repeated data issues to operational memory.

## Operational Memory

Missing livestream data should be treated as a recurring operational risk.

When future sessions are created, Vesper should remind assistants to complete required fields before the session is marked as ready for reporting.
```

## Why This Demo Matters

This demo shows how Vesper may turn data quality problems into structured operational work.

A simple chatbot may say that data is missing.

Vesper should eventually help the team:

- Detect missing fields
- Link missing data to a session
- Link the session to an assistant
- Create follow-up tasks
- Trigger training tasks
- Improve SOPs
- Generate weekly data quality reviews
- Store repeated issues as operational memory

This matters because operational intelligence depends on reliable data.

Bad data produces weak reports.

Reliable data helps Vesper understand what actually happened.

## Public Boundary

This demo is public and synthetic.

It does not include:

- Real customer data
- Real partner information
- Internal screenshots
- Raw interview records
- Private business plans
- Real salary details
- Real recruiting channels
- Production configuration
- API keys or tokens
- Server paths
- Confidential implementation details

## Status

This is an early public demo.

The private implementation may evolve separately as Vesper continues to develop its MCN module, people system, object system, workflow engine, approval layer, data quality layer, and reporting structure.
