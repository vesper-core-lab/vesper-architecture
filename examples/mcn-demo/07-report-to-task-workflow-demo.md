# Report to Task Workflow Demo

This is a synthetic, non-sensitive demo for Vesper's MCN LiveOps module.

It shows how Vesper may transform a weekly report into structured follow-up tasks, review items, approval checkpoints, and operational memory.

This demo does not include real customer data, real partner information, internal screenshots, raw interviews, salary details, recruiting channels, production configuration, server paths, or confidential business workflows.

## Scenario

A MCN operations team generates a weekly LiveOps report.

The report contains several operational signals:

- One livestream session has missing data.
- One campaign needs performance review.
- One host needs training follow-up.
- One assistant needs data quality improvement.
- One SOP may need to be updated.
- Some issues may need manager approval before action.

The goal is to show how Vesper may convert report findings into structured tasks.

A simple chatbot may summarize the report.

Vesper should eventually help turn the report into an executable workflow.

## Synthetic Input

A user may tell Vesper:

```text
Generate follow-up tasks from this weekly report.

Period: 2026-04-13 to 2026-04-19

Report findings:

1. demo_home_account has one livestream session with missing end time and missing duration.
2. Demo Health Supplement campaign needs baseline review.
3. Creator A received repeated feedback about weak product explanation.
4. Operator B has repeated missing data fields across livestream records.
5. The host product explanation SOP may need improvement.
6. The assistant livestream data recording checklist may need improvement.
```

## Expected Vesper Interpretation

Vesper should identify that the report contains several task-generating signals:

- Data completion task
- Campaign review task
- Host training task
- Assistant data quality training task
- SOP improvement task
- Manager review / approval task
- Operational memory update

## Object 1: Weekly Report

```json
{
  "object_type": "report",
  "report_id": "REPORT-WEEK-20260413-20260419",
  "report_type": "weekly_mcn_liveops_report",
  "period_start": "2026-04-13",
  "period_end": "2026-04-19",
  "status": "generated",
  "summary": "Weekly MCN LiveOps report containing data quality issues, campaign review needs, host training signals, assistant data quality issues, and SOP improvement opportunities."
}
```

## Object 2: Report Finding List

```json
{
  "object_type": "report_finding_list",
  "report_id": "REPORT-WEEK-20260413-20260419",
  "findings": [
    {
      "finding_id": "FINDING-001",
      "type": "missing_livestream_data",
      "severity": "high",
      "linked_object_type": "live_session",
      "linked_object_id": "LS-20260416-demo-home"
    },
    {
      "finding_id": "FINDING-002",
      "type": "campaign_baseline_review_needed",
      "severity": "medium",
      "linked_object_type": "campaign",
      "linked_object_id": "CAMPAIGN-202604-health-test"
    },
    {
      "finding_id": "FINDING-003",
      "type": "host_training_needed",
      "severity": "medium",
      "linked_object_type": "host_profile",
      "linked_object_id": "HOST-CREATOR-A"
    },
    {
      "finding_id": "FINDING-004",
      "type": "assistant_data_quality_issue",
      "severity": "high",
      "linked_object_type": "assistant_profile",
      "linked_object_id": "ASSISTANT-OPERATOR-B"
    },
    {
      "finding_id": "FINDING-005",
      "type": "sop_improvement_needed",
      "severity": "medium",
      "linked_object_type": "sop_item",
      "linked_object_id": "SOP-HOST-PRODUCT-EXPLANATION"
    },
    {
      "finding_id": "FINDING-006",
      "type": "sop_improvement_needed",
      "severity": "medium",
      "linked_object_type": "sop_item",
      "linked_object_id": "SOP-ASSISTANT-LIVESTREAM-DATA-RECORDING"
    }
  ]
}
```

## Object 3: Data Completion Task

```json
{
  "object_type": "task",
  "task_id": "TASK-REPORT-DATA-COMPLETE-001",
  "title": "Complete missing livestream data for demo_home_account",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "linked_finding_id": "FINDING-001",
  "linked_object_type": "live_session",
  "linked_object_id": "LS-20260416-demo-home",
  "assigned_role": "assistant",
  "priority": "high",
  "status": "pending",
  "reason": "The weekly report identified missing end time and missing duration for a livestream session."
}
```

## Object 4: Campaign Review Task

```json
{
  "object_type": "task",
  "task_id": "TASK-REPORT-CAMPAIGN-REVIEW-001",
  "title": "Review campaign baseline for Demo Health Supplement",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "linked_finding_id": "FINDING-002",
  "linked_object_type": "campaign",
  "linked_object_id": "CAMPAIGN-202604-health-test",
  "assigned_role": "operator",
  "priority": "medium",
  "status": "pending",
  "reason": "The weekly report identified that the campaign needs a baseline review."
}
```

## Object 5: Host Training Task

```json
{
  "object_type": "training_task",
  "task_id": "TASK-REPORT-HOST-TRAINING-001",
  "title": "Practice product explanation for Creator A",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "linked_finding_id": "FINDING-003",
  "linked_object_type": "host_profile",
  "linked_object_id": "HOST-CREATOR-A",
  "assigned_role": "trainer",
  "priority": "medium",
  "status": "pending",
  "reason": "The weekly report identified repeated feedback about weak product explanation."
}
```

## Object 6: Assistant Data Quality Training Task

```json
{
  "object_type": "training_task",
  "task_id": "TASK-REPORT-ASSISTANT-DQ-001",
  "title": "Complete assistant data quality checklist training",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "linked_finding_id": "FINDING-004",
  "linked_object_type": "assistant_profile",
  "linked_object_id": "ASSISTANT-OPERATOR-B",
  "assigned_role": "trainer",
  "priority": "high",
  "status": "pending",
  "reason": "The weekly report identified repeated missing fields in livestream records."
}
```

## Object 7: Host SOP Improvement Task

```json
{
  "object_type": "task",
  "task_id": "TASK-REPORT-SOP-HOST-001",
  "title": "Improve host product explanation SOP",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "linked_finding_id": "FINDING-005",
  "linked_object_type": "sop_item",
  "linked_object_id": "SOP-HOST-PRODUCT-EXPLANATION",
  "assigned_role": "manager",
  "priority": "medium",
  "status": "pending",
  "reason": "The weekly report identified that product explanation issues may require SOP improvement."
}
```

## Object 8: Assistant SOP Improvement Task

```json
{
  "object_type": "task",
  "task_id": "TASK-REPORT-SOP-ASSISTANT-001",
  "title": "Improve assistant livestream data recording SOP",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "linked_finding_id": "FINDING-006",
  "linked_object_type": "sop_item",
  "linked_object_id": "SOP-ASSISTANT-LIVESTREAM-DATA-RECORDING",
  "assigned_role": "manager",
  "priority": "high",
  "status": "pending",
  "reason": "The weekly report identified repeated assistant data quality issues."
}
```

## Object 9: Approval Checkpoint

Some tasks may require human approval before execution.

```json
{
  "object_type": "approval_checkpoint",
  "approval_id": "APPROVAL-REPORT-WEEK-20260413-20260419",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "tasks_requiring_approval": [
    "TASK-REPORT-SOP-HOST-001",
    "TASK-REPORT-SOP-ASSISTANT-001"
  ],
  "approval_reason": "SOP changes may affect repeated team workflows and should be reviewed by a manager before execution.",
  "status": "pending_manager_review"
}
```

## Object 10: Operational Memory Update

```json
{
  "object_type": "operational_memory",
  "memory_id": "MEMORY-REPORT-TO-TASK-WEEKLY-LOOP",
  "memory_type": "report_to_task_pattern",
  "linked_report_id": "REPORT-WEEK-20260413-20260419",
  "summary": "Weekly reports should not only summarize operations. They should generate follow-up tasks for missing data, campaign review, host training, assistant data quality, SOP improvement, and manager approval.",
  "recommended_use": "Use this memory when processing future weekly reports and converting findings into task workflows.",
  "status": "active"
}
```

## Workflow Linkage

Vesper should connect the report-to-task workflow like this:

```text
Weekly Report
→ Report Findings
→ Task Generation
→ Training Tasks
→ SOP Improvement Tasks
→ Approval Checkpoint
→ Operational Memory
```

The important idea is that reports should not become static documents.

Reports should become operational triggers.

## Example Task Generation Rule

Vesper may use simple public demo rules such as:

```json
{
  "rules": [
    {
      "if": "finding.type == missing_livestream_data",
      "then": "create_data_completion_task"
    },
    {
      "if": "finding.type == campaign_baseline_review_needed",
      "then": "create_campaign_review_task"
    },
    {
      "if": "finding.type == host_training_needed",
      "then": "create_host_training_task"
    },
    {
      "if": "finding.type == assistant_data_quality_issue",
      "then": "create_assistant_training_task"
    },
    {
      "if": "finding.type == sop_improvement_needed",
      "then": "create_sop_improvement_task"
    },
    {
      "if": "task.affects_sop == true",
      "then": "require_manager_approval"
    }
  ]
}
```

## Example Vesper Response

Vesper may respond:

```text
Weekly report processed.

Report:
REPORT-WEEK-20260413-20260419

Findings detected:
6

Tasks created:
6

High priority:
- Complete missing livestream data for demo_home_account
- Complete assistant data quality checklist training
- Improve assistant livestream data recording SOP

Medium priority:
- Review campaign baseline for Demo Health Supplement
- Practice product explanation for Creator A
- Improve host product explanation SOP

Approval required:
2 SOP improvement tasks require manager review.

Operational memory updated:
Weekly report findings should generate structured follow-up tasks.
```

## Example Generated Task Board

Vesper may generate a simple task board.

```markdown
# Weekly Follow-up Task Board

Report: REPORT-WEEK-20260413-20260419

## High Priority

- Complete missing livestream data for demo_home_account
- Complete assistant data quality checklist training
- Improve assistant livestream data recording SOP

## Medium Priority

- Review campaign baseline for Demo Health Supplement
- Practice product explanation for Creator A
- Improve host product explanation SOP

## Approval Needed

- Improve host product explanation SOP
- Improve assistant livestream data recording SOP

## Notes

The report generated tasks across data quality, campaign review, host training, assistant training, SOP improvement, and approval review.

These tasks should be tracked until completed.
```

## Why This Demo Matters

This demo shows how Vesper may turn reports into action.

A simple chatbot may generate a report.

Vesper should eventually help the team:

- Detect findings inside reports
- Classify findings by severity
- Link findings to objects
- Generate tasks
- Assign tasks to roles
- Mark approval requirements
- Track task status
- Store repeated patterns as operational memory

This matters because reports alone do not improve operations.

Actionable task loops improve operations.

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

The private implementation may evolve separately as Vesper continues to develop its MCN module, people system, object system, workflow engine, approval layer, data quality layer, task system, and reporting structure.
