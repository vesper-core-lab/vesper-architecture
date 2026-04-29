# MCN LiveOps Public Model
 
Vesper's first industry validation direction is MCN and cross-border livestream operations.
 
This public note describes a synthetic, non-sensitive model for how Vesper may support livestream operation workflows.
 
It does not include private customer data, internal business documents, raw interviews, production configurations, or real partner information.
 
## Why MCN LiveOps
 
MCN livestream operations are not only about creators and products.
 
A real operation may involve:
 
- Accounts
- Hosts / creators
- Assistants / operators
- Products
- Campaigns
- Livestream sessions
- Stream metrics
- Labor cost
- Profit snapshots
- Feedback records
- Reports
- Follow-up tasks
 
This makes MCN LiveOps a useful early validation scenario for Vesper's object-based operating system design.
 
## Core Public Objects
 
### Account
 
Represents a livestream account, store account, or platform account.
 
Example fields:
 
- account_id
- account_name
- platform
- category
- status
- notes
 
### Creator / Host
 
Represents a host, creator, or livestream performer.
 
Example fields:
 
- creator_id
- name
- role
- language
- status
- linked_accounts
- notes
 
### Assistant / Operator
 
Represents an operational support role.
 
Example fields:
 
- operator_id
- name
- role
- availability
- linked_sessions
- notes
 
### LiveSession
 
Represents a livestream session.
 
Example fields:
 
- live_session_id
- date
- account_id
- host_id
- assistant_id
- campaign_id
- start_time
- end_time
- duration_hours
- status
- data_quality
 
### StreamMetric
 
Represents livestream performance data.
 
Example fields:
 
- metric_id
- live_session_id
- total_gmv
- items_sold
- stream_hours
- viewer_count
- click_count
- conversion_signal
- data_quality
- source
 
### FeedbackRecord
 
Represents a review or improvement record after a livestream session.
 
Example fields:
 
- feedback_id
- live_session_id
- issue
- observation
- suggested_action
- status
- linked_task_id
 
### LaborCost
 
Represents human cost related to a livestream session.
 
Example fields:
 
- labor_cost_id
- live_session_id
- host_cost
- assistant_cost
- operator_cost
- total_labor_cost
- currency
 
### ProfitSnapshot
 
Represents a simplified profit or margin view.
 
Example fields:
 
- profit_id
- live_session_id
- gmv
- product_cost
- labor_cost
- platform_fee
- estimated_profit
- data_quality
 
### Report
 
Represents a structured summary generated from objects and metrics.
 
Example fields:
 
- report_id
- report_type
- period
- linked_sessions
- summary
- risks
- suggested_actions
 
### Task
 
Represents follow-up work generated from operational signals.
 
Example fields:
 
- task_id
- title
- linked_object_type
- linked_object_id
- priority
- status
- reason
 
## Example Workflow
 
A simplified MCN LiveOps workflow may look like this:
 
```text
Account
→ LiveSession
→ StreamMetric
→ FeedbackRecord
→ Report
→ Task
```
 
A more complete workflow may look like this:
 
```text
Campaign
→ Product
→ Creator / Host
→ LiveSession
→ StreamMetric
→ FeedbackRecord
→ Report
→ Follow-up Task
```
 
## Example Operational Logic
 
Vesper should eventually support logic such as:
 
- If livestream data is missing, create a data completion task.
- If GMV is below the expected baseline, create a review task.
- If stream duration is missing, mark the session as `needs_review`.
- If conversion is weak, link the issue to host performance, product fit, or scene quality.
- If repeated issues appear, generate a training or SOP improvement recommendation.
 
## Why This Matters
 
MCN operations are dynamic, people-dependent, and data-sensitive.
 
A simple chatbot can answer questions.
 
A stronger AI Agent Operating System should help structure the operation itself.
 
Vesper's goal is to help connect:
 
- People
- Objects
- Sessions
- Metrics
- Decisions
- Reports
- Tasks
- Memory
 
This is why MCN LiveOps is a useful early scenario for Vesper's object-based workflow architecture.
 
## From Activity Tracking to Operational Intelligence
 
A basic system may only count activity:
 
- Number of livestream sessions
- Number of hours streamed
- Number of products promoted
- Number of reports generated
- Number of tasks completed
 
Vesper should eventually go deeper.
 
It should help understand operational impact:
 
- Did a session improve the state of an account?
- Did a host become more stable after training?
- Did a product show stronger conversion potential?
- Did a feedback record lead to a useful task?
- Did a repeated issue become part of operational memory?
- Did the system reduce uncertainty for the team?
 
The long-term goal is not only to store livestream records.
 
The goal is to help transform fragmented operational activity into structured operational intelligence.
 
## Public Demo Direction
 
This public model can support future synthetic demos such as:
 
- Create a livestream session
- Record livestream metrics
- Detect missing data
- Generate a feedback record
- Create a follow-up task
- Produce a weekly MCN LiveOps report
 
All demos should use synthetic data only.
 
No real customer data, partner information, internal screenshots, raw interview records, or private business workflows should be included.
 
## Public Boundary
 
This document is public and synthetic.
 
It does not include:
 
- Real customer data
- Internal partner documents
- Raw interview records
- Private business plans
- Production configuration
- API keys or tokens
- Server paths
- Confidential implementation details
 
## Status
 
This document is an early public model.
 
The private implementation may evolve separately as Vesper continues to develop its MCN module, object system, workflow engine, approval layer, and reporting structure.
