# One Sentence to Operation

## Core Idea

Most AI agents answer questions.

Vesper structures operations.

This demo shows how Vesper turns one business question into operational objects, reports, follow-up tasks, and approval boundaries.

## User Input

> Why is this livestream not converting?

Or in Chinese:

> 这个直播为什么卖不动？

## Vesper Interpretation

Vesper does not treat this as a normal chat question.

It interprets the input as an operational investigation request.

The goal is not only to answer the question, but to structure the operation behind it.

## Objects Involved

Vesper maps the question to operational objects:

- Product
- Campaign
- Creator / Host
- LiveSession
- Order
- Report
- Task
- Approval Checkpoint

## Step 1: Find Related Objects

Vesper checks:

- Which product was promoted
- Which campaign the product belongs to
- Which livestream session generated the result
- Whether orders were created
- Whether feedback records exist
- Whether follow-up tasks already exist

## Step 2: Generate Report

Example report:

{
  "report_type": "livestream_conversion_check",
  "livestream_id": "LIVE-demo-001",
  "product": "Demo Water Cup",
  "campaign": "Summer Promotion",
  "orders": 12,
  "revenue": 1188,
  "average_order_value": 99,
  "conversion_signal": "weak",
  "possible_issue": "traffic-to-order drop"
}

## Step 3: Identify Possible Causes

Vesper may identify:

- The host explained the product too late
- The opening script did not create urgency
- Audience questions were not converted into purchase prompts
- The product benefit was not repeated clearly
- The campaign lacked a strong call-to-action

## Step 4: Generate Follow-up Tasks

Example tasks:

[
  {
    "task_type": "script_review",
    "target": "opening_script",
    "priority": "high",
    "status": "pending"
  },
  {
    "task_type": "host_training",
    "target": "conversion_prompting",
    "priority": "medium",
    "status": "pending"
  },
  {
    "task_type": "campaign_review",
    "target": "call_to_action",
    "priority": "medium",
    "status": "pending"
  }
]

## Step 5: Approval Boundary

Vesper does not automatically change the campaign.

It proposes actions and waits for human approval.

Human approval is required before:

- Changing campaign strategy
- Assigning training tasks
- Updating SOP
- Sending instructions to creators or operators
- Triggering any external execution

## Final Response Example

Vesper Operational Draft:

Problem:
The livestream appears to have weak conversion.

Observed signals:
- Orders are lower than expected.
- Revenue is limited.
- Average order value is stable.
- The issue may be traffic-to-order conversion.

Suggested checks:
1. Review the opening script.
2. Check whether the host explained the product benefit clearly.
3. Review audience questions during the livestream.
4. Compare this session with stronger sessions.
5. Generate a host training task if approved.

Status:
This is a read-only operational draft.
No task has been executed.
Human approval is required for next actions.

## Why This Matters

A chatbot gives an answer.

Vesper builds an operation.
