# Host Training Feedback Workflow Demo

This is a synthetic, non-sensitive demo for Vesper's MCN LiveOps module.

It shows how Vesper may connect a host profile, livestream session, feedback record, training task, SOP improvement, and review snapshot into a structured people-development workflow.

This demo does not include real customer data, real partner information, internal screenshots, raw interviews, salary details, recruiting channels, production configuration, server paths, or confidential business workflows.

## Scenario

A MCN operations team wants to improve livestream host performance over time.

The team does not only want to record livestream results.

The team wants to understand:

- Which host needs training
- Which issue appeared during a session
- Whether the issue is repeated
- Whether the issue should create a training task
- Whether the SOP should be improved
- Whether the host is becoming more stable over time
- Whether the feedback should become operational memory

The goal is to show how Vesper may help transform scattered feedback into structured training and review workflows.

## Synthetic Input

A user may tell Vesper:

```text
Record host feedback after a livestream session.

Host: Creator A
Account: demo_health_account
Session: LS-20260415-demo-health
Date: 2026-04-15

Observation:
The host completed the session, but the product explanation was unclear during the first 20 minutes.

Issue:
Weak product explanation.

Suggested action:
Create a training task for product explanation practice.

Training priority: medium
```

## Expected Vesper Interpretation

Vesper should identify that this input contains several connected objects:

- HostProfile
- Account
- LiveSession
- FeedbackRecord
- TrainingTask
- SOPItem
- ReviewSnapshot
- OperationalMemory

## Object 1: HostProfile

```json
{
  "object_type": "host_profile",
  "host_id": "HOST-CREATOR-A",
  "person_id": "PERSON-CREATOR-A",
  "name": "Creator A",
  "role": "host",
  "language": "en",
  "category_fit": [
    "health",
    "lifestyle"
  ],
  "training_stage": "live_session_support",
  "performance_level": "developing",
  "status": "active"
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

## Object 3: LiveSession

```json
{
  "object_type": "live_session",
  "live_session_id": "LS-20260415-demo-health",
  "date": "2026-04-15",
  "account_id": "ACC-demo-health",
  "host_id": "HOST-CREATOR-A",
  "duration_hours": 2.0,
  "status": "completed",
  "data_quality": "valid"
}
```

## Object 4: FeedbackRecord

```json
{
  "object_type": "feedback_record",
  "feedback_id": "FB-HOST-CREATOR-A-20260415",
  "linked_person_id": "PERSON-CREATOR-A",
  "linked_host_id": "HOST-CREATOR-A",
  "linked_session_id": "LS-20260415-demo-health",
  "issue": "weak_product_explanation",
  "observation": "The host completed the session, but the product explanation was unclear during the first 20 minutes.",
  "suggested_action": "Create a training task for product explanation practice.",
  "status": "open"
}
```

## Object 5: TrainingTask

```json
{
  "object_type": "training_task",
  "task_id": "TRAINING-HOST-CREATOR-A-PRODUCT-EXPLANATION",
  "person_id": "PERSON-CREATOR-A",
  "host_id": "HOST-CREATOR-A",
  "title": "Practice product explanation for health livestream sessions",
  "reason": "Feedback record identified weak product explanation during livestream session.",
  "priority": "medium",
  "status": "pending",
  "linked_feedback_id": "FB-HOST-CREATOR-A-20260415"
}
```

## Object 6: SOPItem

```json
{
  "object_type": "sop_item",
  "sop_id": "SOP-HOST-PRODUCT-EXPLANATION",
  "title": "Host product explanation checklist",
  "category": "host_training",
  "description": "A checklist for explaining product value, usage scenario, key benefits, and audience objections during livestream sessions.",
  "linked_role": "host",
  "status": "draft",
  "version": "0.1"
}
```

## Object 7: ReviewSnapshot

```json
{
  "object_type": "review_snapshot",
  "review_id": "REVIEW-HOST-CREATOR-A-20260415",
  "person_id": "PERSON-CREATOR-A",
  "host_id": "HOST-CREATOR-A",
  "period": "2026-04-15",
  "strengths": [
    "Completed the livestream session",
    "Maintained session flow"
  ],
  "risks": [
    "Product explanation needs improvement"
  ],
  "repeated_issues": [
    "weak_product_explanation"
  ],
  "suggested_actions": [
    "Complete product explanation practice",
    "Use host product explanation checklist in next session"
  ],
  "status": "open"
}
```

## Object 8: OperationalMemory

```json
{
  "object_type": "operational_memory",
  "memory_id": "MEMORY-HOST-TRAINING-PRODUCT-EXPLANATION",
  "memory_type": "training_pattern",
  "linked_role": "host",
  "issue": "weak_product_explanation",
  "summary": "Hosts may need structured product explanation practice before livestream sessions, especially when promoting products that require education or trust-building.",
  "recommended_use": "Use this memory when preparing host training tasks or SOP improvements for product-heavy livestream sessions.",
  "status": "active"
}
```

## Workflow Linkage

Vesper should connect the people-development workflow like this:

```text
HostProfile
→ LiveSession
→ FeedbackRecord
→ TrainingTask
→ SOPItem
→ ReviewSnapshot
→ OperationalMemory
```

The important idea is that feedback should not disappear in chat history.

Feedback should become structured improvement work.

## Example Operational Check

Vesper may run simple checks.

```json
{
  "check_result": "needs_training_task",
  "linked_objects": {
    "host_profile": true,
    "live_session": true,
    "feedback_record": true,
    "training_task": true,
    "sop_item": true,
    "review_snapshot": true
  },
  "issue_detected": "weak_product_explanation",
  "recommended_action": "Create or update host training task and SOP checklist."
}
```

## Example Vesper Response

Vesper may respond:

```text
Feedback recorded.

Linked host:
Creator A

Linked session:
LS-20260415-demo-health

Detected issue:
Weak product explanation

Created training task:
Practice product explanation for health livestream sessions

Suggested SOP update:
Create or improve host product explanation checklist

Review status:
Open

This feedback may become part of operational memory if the same issue appears repeatedly.
```

## Repeated Issue Example

If similar feedback appears across multiple sessions, Vesper should detect a repeated pattern.

Example repeated feedback records:

```json
[
  {
    "feedback_id": "FB-HOST-CREATOR-A-20260415",
    "issue": "weak_product_explanation",
    "linked_session_id": "LS-20260415-demo-health"
  },
  {
    "feedback_id": "FB-HOST-CREATOR-A-20260418",
    "issue": "weak_product_explanation",
    "linked_session_id": "LS-20260418-demo-health"
  },
  {
    "feedback_id": "FB-HOST-CREATOR-B-20260419",
    "issue": "weak_product_explanation",
    "linked_session_id": "LS-20260419-demo-health"
  }
]
```

Expected system signal:

```json
{
  "check_result": "repeated_issue_detected",
  "issue": "weak_product_explanation",
  "affected_hosts": [
    "HOST-CREATOR-A",
    "HOST-CREATOR-B"
  ],
  "recommended_action": "Create SOP improvement task and update training material."
}
```

## Example SOP Improvement Task

```json
{
  "object_type": "task",
  "task_id": "TASK-SOP-IMPROVE-PRODUCT-EXPLANATION",
  "title": "Improve host product explanation SOP",
  "linked_object_type": "sop_item",
  "linked_object_id": "SOP-HOST-PRODUCT-EXPLANATION",
  "priority": "high",
  "status": "pending",
  "reason": "Repeated feedback indicates that multiple hosts need clearer product explanation structure."
}
```

## Example Weekly People Review

Vesper may generate a weekly people and training review.

```markdown
# Weekly Host Training Review

Period: 2026-04-13 to 2026-04-19

## Summary

This week includes repeated feedback related to product explanation quality.

Affected hosts:

- Creator A
- Creator B

## Key Issue

Weak product explanation appeared in multiple livestream sessions.

## Training Actions

- Create product explanation practice task for affected hosts.
- Review host script structure before future sessions.
- Add product value explanation checklist to session preparation.

## SOP Actions

- Improve host product explanation SOP.
- Add examples for product benefits, use cases, objections, and audience trust-building.
- Review the SOP after two more sessions.

## Operational Memory

This issue should be stored as a training pattern.

When future health or education-heavy products are promoted, Vesper should remind the team to prepare host product explanation training in advance.
```

## Why This Demo Matters

This demo shows how Vesper may move from feedback collection to people development.

A simple chatbot may summarize feedback.

Vesper should eventually structure feedback into:

- Training tasks
- SOP updates
- Review snapshots
- Repeated issue detection
- Operational memory
- Future preparation signals

This is important because MCN operations depend on people.

People improve through structured feedback, training, repetition, and review.

The goal is not only to record what happened.

The goal is to help the organization learn.

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

The private implementation may evolve separately as Vesper continues to develop its MCN module, people system, object system, workflow engine, approval layer, and reporting structure.
