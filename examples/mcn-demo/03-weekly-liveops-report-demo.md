# Weekly LiveOps Report Demo

This is a synthetic, non-sensitive demo for Vesper's MCN LiveOps module.

It shows how Vesper may summarize multiple livestream sessions into a weekly operational report.

This demo does not include real customer data, real partner information, internal screenshots, raw interviews, production configuration, server paths, or confidential business workflows.

## Scenario

A MCN operations team runs multiple livestream sessions during one week.

The team wants Vesper to summarize:

- Total stream hours
- Total GMV
- Total items sold
- GMV per hour
- Items sold per hour
- Data quality issues
- Session-level observations
- Follow-up tasks
- Operational risks
- Suggested improvements

The goal is not only to count activity.

The goal is to help the team understand operational impact.

## Synthetic Weekly Input

A user may tell Vesper:

```text
Generate a weekly MCN LiveOps report.

Period: 2026-04-13 to 2026-04-19

Session 1:
Date: 2026-04-15
Account: demo_health_account
Host: Creator A
Assistant: Operator B
Duration: 2.0 hours
GMV: 1200.00
Items Sold: 38
Data Quality: valid

Session 2:
Date: 2026-04-16
Account: demo_home_account
Host: Creator B
Assistant: Operator B
Duration: 1.5 hours
GMV: 0.00
Items Sold: 0
Data Quality: missing

Session 3:
Date: 2026-04-18
Account: demo_beauty_account
Host: Creator C
Assistant: Operator D
Duration: 2.5 hours
GMV: 2600.00
Items Sold: 74
Data Quality: valid
```

## Expected Vesper Interpretation

Vesper should identify that this weekly input contains:

- Multiple LiveSession objects
- Multiple StreamMetric objects
- Account-level performance
- Host-level performance
- Assistant-level data quality signals
- Missing data risks
- Weekly report summary
- Follow-up tasks

## Synthetic LiveSession Objects

```json
[
  {
    "object_type": "live_session",
    "live_session_id": "LS-20260415-demo-health",
    "date": "2026-04-15",
    "account_id": "ACC-demo-health",
    "host_id": "CREATOR-A",
    "assistant_id": "OPERATOR-B",
    "duration_hours": 2.0,
    "status": "completed",
    "data_quality": "valid"
  },
  {
    "object_type": "live_session",
    "live_session_id": "LS-20260416-demo-home",
    "date": "2026-04-16",
    "account_id": "ACC-demo-home",
    "host_id": "CREATOR-B",
    "assistant_id": "OPERATOR-B",
    "duration_hours": 1.5,
    "status": "needs_review",
    "data_quality": "missing"
  },
  {
    "object_type": "live_session",
    "live_session_id": "LS-20260418-demo-beauty",
    "date": "2026-04-18",
    "account_id": "ACC-demo-beauty",
    "host_id": "CREATOR-C",
    "assistant_id": "OPERATOR-D",
    "duration_hours": 2.5,
    "status": "completed",
    "data_quality": "valid"
  }
]
```

## Synthetic StreamMetric Objects

```json
[
  {
    "object_type": "stream_metric",
    "metric_id": "METRIC-LS-20260415-demo-health",
    "live_session_id": "LS-20260415-demo-health",
    "total_gmv": 1200.00,
    "items_sold": 38,
    "stream_hours": 2.0,
    "gmv_per_hour": 600.00,
    "items_sold_per_hour": 19,
    "data_quality": "valid"
  },
  {
    "object_type": "stream_metric",
    "metric_id": "METRIC-LS-20260416-demo-home",
    "live_session_id": "LS-20260416-demo-home",
    "total_gmv": 0.00,
    "items_sold": 0,
    "stream_hours": 1.5,
    "gmv_per_hour": 0.00,
    "items_sold_per_hour": 0,
    "data_quality": "missing"
  },
  {
    "object_type": "stream_metric",
    "metric_id": "METRIC-LS-20260418-demo-beauty",
    "live_session_id": "LS-20260418-demo-beauty",
    "total_gmv": 2600.00,
    "items_sold": 74,
    "stream_hours": 2.5,
    "gmv_per_hour": 1040.00,
    "items_sold_per_hour": 29.6,
    "data_quality": "valid"
  }
]
```

## Weekly Summary Calculation

Vesper may calculate a weekly summary.

```json
{
  "object_type": "weekly_liveops_summary",
  "period_start": "2026-04-13",
  "period_end": "2026-04-19",
  "total_sessions": 3,
  "total_stream_hours": 6.0,
  "total_gmv": 3800.00,
  "total_items_sold": 112,
  "average_gmv_per_hour": 633.33,
  "average_items_sold_per_hour": 18.67,
  "valid_sessions": 2,
  "sessions_needing_review": 1,
  "data_quality": "partial"
}
```

## Data Quality Check

Vesper should detect incomplete or risky records.

```json
{
  "check_result": "needs_review",
  "issues": [
    {
      "live_session_id": "LS-20260416-demo-home",
      "issue_type": "missing_or_zero_performance",
      "description": "The session has missing data quality and zero GMV / zero items sold.",
      "recommended_action": "Create a review task and verify whether the performance data is complete."
    }
  ]
}
```

## Example Feedback Records

```json
[
  {
    "object_type": "feedback_record",
    "feedback_id": "FB-LS-20260416-demo-home",
    "live_session_id": "LS-20260416-demo-home",
    "issue": "missing_or_zero_performance",
    "observation": "The session has zero GMV and zero items sold, while data quality is marked as missing.",
    "suggested_action": "Verify data completeness and review session execution.",
    "status": "open"
  },
  {
    "object_type": "feedback_record",
    "feedback_id": "FB-WEEK-20260413",
    "linked_period": "2026-04-13_to_2026-04-19",
    "issue": "weekly_baseline_needed",
    "observation": "The week contains valid sessions and one missing-quality session. More weeks are needed to establish reliable account and host baselines.",
    "suggested_action": "Continue tracking GMV per hour, items sold per hour, data quality, host stability, and assistant recording quality.",
    "status": "open"
  }
]
```

## Example Follow-up Tasks

```json
[
  {
    "object_type": "task",
    "task_id": "TASK-DATA-CHECK-LS-20260416-demo-home",
    "title": "Review missing or zero performance data for demo_home_account",
    "linked_object_type": "live_session",
    "linked_object_id": "LS-20260416-demo-home",
    "priority": "high",
    "status": "pending",
    "reason": "Session has missing data quality and zero GMV / items sold."
  },
  {
    "object_type": "task",
    "task_id": "TASK-WEEKLY-BASELINE-20260413",
    "title": "Build weekly baseline for MCN LiveOps performance",
    "linked_object_type": "weekly_liveops_summary",
    "linked_object_id": "WEEK-20260413-20260419",
    "priority": "medium",
    "status": "pending",
    "reason": "The system needs more weekly data to compare account, host, and session performance."
  }
]
```

## Example Weekly Report

Vesper may generate a weekly report.

```markdown
# Weekly MCN LiveOps Report

Period: 2026-04-13 to 2026-04-19

## Summary

This week contains 3 livestream sessions.

Total stream hours: 6.0  
Total GMV: 3800.00  
Total items sold: 112  
Average GMV per hour: 633.33  
Average items sold per hour: 18.67  

Data quality status: partial

## Session Overview

### Session 1

- Date: 2026-04-15
- Account: demo_health_account
- Host: Creator A
- Assistant: Operator B
- Duration: 2.0 hours
- GMV: 1200.00
- Items sold: 38
- GMV per hour: 600.00
- Data quality: valid

### Session 2

- Date: 2026-04-16
- Account: demo_home_account
- Host: Creator B
- Assistant: Operator B
- Duration: 1.5 hours
- GMV: 0.00
- Items sold: 0
- GMV per hour: 0.00
- Data quality: missing
- Status: needs review

### Session 3

- Date: 2026-04-18
- Account: demo_beauty_account
- Host: Creator C
- Assistant: Operator D
- Duration: 2.5 hours
- GMV: 2600.00
- Items sold: 74
- GMV per hour: 1040.00
- Data quality: valid

## Observations

The week contains two valid sessions and one session that needs review.

The strongest synthetic session is demo_beauty_account, with the highest GMV per hour.

The demo_home_account session requires review because performance is zero and data quality is missing.

## Suggested Actions

- Verify whether demo_home_account has complete data.
- Compare Creator C performance with future sessions.
- Track Assistant / Operator data recording quality across sessions.
- Continue building account-level and host-level baselines.
- Convert repeated data issues into SOP improvements.

## Generated Follow-up Tasks

- Review missing or zero performance data for demo_home_account.
- Build weekly baseline for MCN LiveOps performance.
```

## Why This Demo Matters

This demo shows how Vesper may transform multiple operational records into a structured weekly report.

A simple chatbot may summarize the records.

Vesper should eventually help the team understand:

- Which sessions performed well
- Which sessions need review
- Which data is missing
- Which tasks should be created
- Which accounts need attention
- Which people or roles may require follow-up
- Which signals should become operational memory

The goal is to move from scattered livestream records to structured operational intelligence.

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
