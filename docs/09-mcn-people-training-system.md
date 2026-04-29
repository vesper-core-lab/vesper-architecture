# MCN People and Training System

Vesper's first industry validation direction is MCN and cross-border livestream operations.

This public note describes a synthetic, non-sensitive model for how Vesper may support people management, training workflows, assistant coordination, review loops, and operational memory in MCN livestream teams.

It does not include private customer data, internal business documents, raw interviews, real partner information, salary details, recruiting channels, production configurations, or confidential workflows.

## Why People Systems Matter

MCN operations are not only about livestream data.

A real livestream operation depends heavily on people.

The system may involve:

- Hosts / creators
- Assistants
- Operators
- Reviewers
- Trainers
- Account managers
- Product coordinators
- Remote managers

The quality of the operation depends on whether these people can be recruited, trained, scheduled, reviewed, and improved over time.

This makes people and training systems an important part of Vesper's MCN module.

## From Individual Performance to Operational Capability

A simple system may only record who joined a livestream.

A stronger operating system should understand how people become more reliable over time.

For example, Vesper should eventually help answer:

- Which host is ready for live sessions?
- Which host needs more training?
- Which assistant can support which type of session?
- Which repeated issues appear across different sessions?
- Which feedback records should become training tasks?
- Which SOP needs to be improved?
- Which team member is overloaded?
- Which workflow requires human approval?

This means the people system should not only store names.

It should connect people to tasks, sessions, feedback, training stages, and operational memory.

## Core Public Objects

### Person

Represents a human participant in the operation.

Example fields:

- person_id
- name
- role
- status
- language
- region
- notes

Possible roles may include:

- host
- creator
- assistant
- operator
- reviewer
- trainer
- manager

### HostProfile

Represents a livestream host or creator profile.

Example fields:

- host_id
- person_id
- language
- category_fit
- training_stage
- performance_level
- linked_accounts
- notes

The purpose of this object is to help Vesper understand host readiness and improvement direction.

### AssistantProfile

Represents an assistant or operator profile.

Example fields:

- assistant_id
- person_id
- role_type
- availability
- supported_accounts
- supported_hosts
- training_stage
- notes

Assistant roles may include:

- live assistant
- session operator
- product coordinator
- data recorder
- review assistant

### TrainingStage

Represents the current training phase of a person.

Example fields:

- training_stage_id
- person_id
- stage_name
- status
- required_skills
- completed_items
- next_actions
- reviewer

Example public stages may include:

- orientation
- basic workflow training
- product and script training
- live session support
- independent execution
- review and improvement

### SOPItem

Represents a standard operating procedure item.

Example fields:

- sop_id
- title
- category
- description
- linked_role
- status
- version
- owner

SOPs may cover:

- livestream preparation
- host checklist
- assistant checklist
- product setup
- data recording
- post-session review
- escalation rules

### FeedbackRecord

Represents a review or improvement note connected to a person, session, or workflow.

Example fields:

- feedback_id
- linked_person_id
- linked_session_id
- issue
- observation
- suggested_action
- status
- linked_task_id

Feedback records are important because they help convert operational problems into structured improvement tasks.

### TrainingTask

Represents a task created for training or improvement.

Example fields:

- task_id
- person_id
- title
- reason
- priority
- status
- due_date
- linked_feedback_id

Training tasks may be created when:

- A host needs script practice.
- An assistant misses a data entry step.
- A repeated issue appears across sessions.
- A SOP is unclear.
- A manager needs to review performance.

### ReviewSnapshot

Represents a structured review of a person or team over a period of time.

Example fields:

- review_id
- person_id
- period
- strengths
- risks
- repeated_issues
- suggested_actions
- reviewer
- status

A review snapshot should help managers understand whether a person is improving, stable, overloaded, or needs intervention.

## Example Workflow

A simplified people and training workflow may look like this:

- Person
- HostProfile or AssistantProfile
- TrainingStage
- LiveSession
- FeedbackRecord
- TrainingTask
- ReviewSnapshot
- Operational Memory

A more complete workflow may look like this:

- Recruit or identify a person
- Create a profile
- Assign a training stage
- Link the person to sessions
- Record feedback
- Generate improvement tasks
- Review progress
- Update SOP or training memory

## Example Operational Logic

Vesper should eventually support logic such as:

- If a host repeatedly underperforms, create a review task.
- If an assistant misses required data fields, create a training task.
- If multiple people fail at the same step, suggest SOP improvement.
- If a person completes required training steps, update training stage.
- If a live session has missing data, link the issue to the responsible workflow role.
- If a person becomes stable across multiple sessions, mark readiness as improved.
- If a repeated issue appears, store it as operational memory.

## Why This Matters

MCN operations are people-dependent.

Without a structured people system, many problems remain hidden in chat messages, spreadsheets, or informal memory.

A simple chatbot can answer questions about people.

A stronger AI Agent Operating System should help structure how people are trained, reviewed, assigned, improved, and connected to workflows.

For Vesper, the goal is not only to record activity.

The goal is to help build operational capability.

## From Training Records to Organizational Memory

A training system should not only store who completed which task.

It should help the organization learn.

Useful memory may include:

- Common host weaknesses
- Common assistant mistakes
- Repeated workflow failures
- Effective training methods
- Useful SOP improvements
- Reliable role assignments
- Risk patterns before live sessions
- Review patterns after live sessions

This kind of memory can help Vesper become more useful over time.

## Public Demo Direction

This public model can support future synthetic demos such as:

- Create a host profile.
- Create an assistant profile.
- Assign a training stage.
- Link a host to a livestream session.
- Record feedback after a session.
- Generate a training task.
- Produce a weekly people and training review.

All demos should use synthetic data only.

No real customer data, partner information, internal screenshots, raw interview records, salary details, recruiting channels, or private business workflows should be included.

## Public Boundary

This document is public and synthetic.

It does not include:

- Real customer data
- Internal partner documents
- Raw interview records
- Private business plans
- Real salary details
- Real recruiting channels
- Production configuration
- API keys or tokens
- Server paths
- Confidential implementation details

## Status

This document is an early public model.

The private implementation may evolve separately as Vesper continues to develop its MCN module, people system, object system, workflow engine, approval layer, and reporting structure.
