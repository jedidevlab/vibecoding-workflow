---
name: vibecoding-workflow
description: Lightweight workflow for starting small software projects from a rough idea. Use when the user wants to turn an idea into a practical development plan, including requirements, detailed design, task breakdown, progress tracking, and an agent launch prompt. Best for small projects that need more structure than ad hoc coding but less process than OpenSpec.
---

# Vibecoding Workflow

Turn a small project idea into a ready-to-execute development context. Produce just enough structure to help an agent build the project without guessing, over-planning, or adopting heavyweight spec governance.

## Fit Check

Use this skill for small projects, prototypes, tools, apps, scripts, dashboards, experiments, and repo-local features where the user needs a clean launch plan.

Do not turn this into OpenSpec-style process. Avoid change ledgers, formal proposal review systems, long lifecycle governance, or enterprise templates unless the user explicitly asks for them.

If the request is already a concrete code change with clear requirements, do the code task directly instead of forcing this workflow.

## Core Principles

- Clarify before specifying. Do not guess user intent.
- Keep the workflow lightweight. Prefer a short useful document over a complete but slow one.
- Stay project-specific. Do not add generic methodology unless it affects the current project.
- Make every task executable. Each task needs scope, expected output, and verification.
- Bind implementation to validation. Prefer tasks that can be independently tested or checked.
- Avoid speculative features, abstractions, tools, and architecture.
- Keep the workflow moving by default. Continue through the next artifact when the current one is sufficiently clear.
- Pause for questions only on decisions that would materially change scope, user experience, data model, architecture, or acceptance criteria.

## Workflow

Follow these stages in order unless the user asks for only one artifact.

### 1. Clarify

Inspect the current project context first when a workspace exists. Read available README files, manifests, docs, and relevant source structure before asking questions.

Ask the minimum useful questions needed to define:

- project goal
- target user or operator
- core workflow
- must-have features
- existing materials such as requirement notes, links, screenshots, datasets, ROMs, API docs, schemas, or reference repos
- current project background such as new project, existing project, repo state, available source, or no source yet
- explicit non-goals
- technical constraints
- acceptance criteria

Prefer one compact batch of questions for a new project. For very small projects, make reasonable assumptions and list them instead of blocking.

### 2. Specify

Create or update `doc/proposal.md`.

Include:

- project summary
- current project background
- existing materials
- users and use cases
- functional requirements
- non-functional requirements
- constraints and assumptions
- out-of-scope items
- acceptance criteria

Keep the proposal practical. Avoid market analysis, long personas, or product strategy unless the user asked for them.

### 3. Design

Create or update `doc/detailed-design.md`.

Include:

- system overview
- existing code or project structure, or explicitly state that none exists
- module or component breakdown
- responsibilities for each module
- key data structures or interfaces
- important flows
- error handling strategy
- testing and verification strategy
- implementation order if it matters

Design for independent work units. Modules should be small enough that an agent can understand and test each one without holding the entire project in context.

Do not introduce capabilities absent from `doc/proposal.md`.

### 4. Plan

Create or update:

- `doc/tasks/<module-name>.md` for each module or workstream
- `doc/tasks/progress.md` for overall progress

Each task file must use checklists and include:

- task objective
- inputs
- expected outputs
- files or areas likely to change
- step-by-step work items
- success criteria
- verification command or manual check
- dependencies on other tasks, if any

Keep tasks small. Split any task that mixes unrelated behavior, requires too many files at once, or lacks a clear verification step.

`progress.md` should show module-level status and the recommended execution order.

### 5. Launch

Create or update `doc/prompt.md`.

The launch prompt should tell the future agent to:

- read `doc/proposal.md`, `doc/detailed-design.md`, and `doc/tasks/progress.md`
- act as the main agent responsible for overall progress, task status, coordination, and phase-level verification
- use subagents only when tasks are independent enough to execute separately
- keep each subagent scoped to one module or one task
- require each subagent to implement the assigned task and complete its listed verification
- continue from one phase to the next when the required context is sufficient
- execute tasks in dependency order
- update checklists as work completes
- keep changes scoped to the active task
- add or update tests proportionally to risk
- run the verification listed for each task
- stop and ask when a requirement, design decision, or acceptance criterion is ambiguous

Do not hard-code a language, framework, test runner, formatter, or type checker unless the proposal or design specifies it.

Suggest validation methods that fit the project, such as:

- unit tests
- integration tests
- type checks
- formatting checks
- static analysis
- build or startup verification
- end-to-end tests
- manual acceptance checks

## Artifact Templates

Use these structures as defaults. Adjust section names only when the project already has a clearer documentation convention.

### `doc/proposal.md`

```markdown
# Proposal

## Project Summary

## Current Project Background

## Existing Materials

## Users and Use Cases

## Functional Requirements

## Non-Functional Requirements

## Constraints and Assumptions

## Out of Scope

## Acceptance Criteria
```

### `doc/detailed-design.md`

```markdown
# Detailed Design

## System Overview

## Existing Code or Project Structure

## Modules and Responsibilities

## Key Data Structures and Interfaces

## Important Flows

## Error Handling

## Testing and Verification Strategy

## Implementation Order
```

### `doc/tasks/<module-name>.md`

```markdown
# <Module Name> Tasks

## Objective

## Inputs

## Expected Outputs

## Likely Files or Areas to Change

## Dependencies

## Tasks

- [ ] ...

## Success Criteria

## Verification
```

### `doc/tasks/progress.md`

```markdown
# Progress

## Recommended Order

## Module Status

- [ ] ...

## Notes and Blockers
```

### `doc/prompt.md`

```markdown
# Agent Launch Prompt

## Goal

## Required Context

## Execution Rules

## Main Agent Responsibilities

## Subagent Rules

## Task Order

## Verification Requirements

## Stop Conditions
```

## Output Rules

When generating the workflow artifacts:

- Use `doc/` unless the existing project clearly uses `docs/`; follow the repo if it already has a convention.
- Use concise Markdown.
- Prefer concrete bullets and checklists over prose-heavy sections.
- Mark assumptions explicitly.
- Keep non-goals visible so later agents do not expand scope.
- Do not overwrite useful existing documentation without first reading and preserving relevant content.

## Completion Check

Before finishing, verify that:

- `proposal.md` has clear acceptance criteria.
- `detailed-design.md` maps requirements to modules or flows.
- every task has a verification method.
- `progress.md` gives an execution order.
- `prompt.md` is usable by a fresh agent without hidden context.
