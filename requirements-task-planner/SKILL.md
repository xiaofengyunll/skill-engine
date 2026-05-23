---
name: requirements-task-planner
description: Write requirement-gathering and task-planning proposals from a product/analysis perspective. Use when Codex needs to collect, clarify, validate, freeze, and organize requirements before producing a task plan, project plan, implementation plan, requirement analysis, delivery roadmap, or technical planning document. Trigger especially when requirements may be ambiguous, incomplete, contradictory, need Quick/Standard/Deep planning modes, or need workflow, class relationship, architecture, state, sequence, or process diagrams represented with Mermaid code.
---

# Requirements Task Planner

## Core Rule

Collect requirements completely before planning. If any requirement is missing, ambiguous, contradictory, or high-risk, ask the user focused follow-up questions first and stop there. Do not produce a task plan until the user's answers make the requirement set complete enough to plan responsibly.

Always keep the current phase visible in reasoning and output. Do not mix requirement discovery, architecture design, and task planning in the same step unless the user explicitly requests a lightweight plan.

## Planning Modes

Default to Standard Mode unless the user asks for speed, the task is clearly small, or ambiguity/complexity requires deeper analysis.

- Quick Mode: Use minimal clarification and lightweight planning for small, low-risk tasks. Ask only blocking questions.
- Standard Mode: Balance requirement collection, validation, task planning, risks, and acceptance criteria.
- Deep Analysis Mode: Use full requirement engineering, assumption confirmation, architecture/design structure, workflows, class or module diagrams, milestones, and risk review.

Escalate from Quick or Standard Mode to Deep Analysis Mode when scope is broad, requirements are unclear, architecture choices are consequential, compliance/security risk exists, or multiple teams/systems are involved.

## Execution Phases

Operate in phases:

1. Requirement Discovery
2. Requirement Validation
3. Assumption Confirmation
4. Solution Structuring
5. Task Planning
6. Risk Review
7. Delivery Proposal

Never skip phases unless the user explicitly requests Quick Mode or a lightweight output. When skipping, state the chosen mode and preserve the boundary between requirement facts, assumptions, design, and tasks.

## Workflow

1. Select the planning mode and state it when useful.
2. Restate the user's goal in concise terms.
3. Extract known requirements into functional requirements, non-functional requirements, constraints, stakeholders, inputs/outputs, data, integrations, acceptance criteria, priorities, and delivery expectations.
4. Identify unknowns, ambiguities, contradictions, assumptions, priority conflicts, and decision points.
5. Ask follow-up questions when needed.
6. Continue requirement collection until all necessary questions are answered or clearly marked as user-approved assumptions.
7. Freeze the requirement set before planning.
8. Only after requirements are complete, write the task planning proposal.

## Requirement Collection

Check these areas before planning:

- Business objective: problem, expected outcome, success metrics.
- Users and roles: primary users, admins, external systems, permission boundaries.
- Scope: in-scope features, out-of-scope features, priorities, MVP boundaries.
- Priority and sequencing: must-have, should-have, nice-to-have, deferred scope.
- Functional behavior: workflows, user actions, system responses, rules, edge cases.
- Data: entities, fields, validation, lifecycle, retention, import/export.
- Integrations: upstream/downstream systems, APIs, authentication, dependencies.
- Non-functional requirements: performance, availability, security, privacy, compliance, observability, scalability, compatibility.
- Delivery constraints: timeline, team, technology stack, deployment environment, budget, migration needs.
- Acceptance criteria: testable completion criteria and review standards.

If requirements are large or unclear, ask the user to prioritize MVP scope, critical workflows, high-risk areas, and deferred features.

## Asking Questions

Ask questions only for information needed to remove planning risk. Keep questions grouped and easy to answer.

Use this format when requirements are incomplete:

```markdown
我还需要确认以下需求后才能开始任务规划：

1. [问题]
2. [问题]
3. [问题]

当前我已理解的需求：
- [已知点]
- [已知点]
```

Prefer 3-7 high-value questions at a time. If many unknowns exist, ask about priority, scope, users, data, and acceptance criteria first.

Do not hide uncertainty as assumptions. Use assumptions only when the user explicitly authorizes proceeding with assumptions, or when the requirement is low-risk and clearly labeled.

## Requirement Freeze Rule

Before entering planning mode, summarize the finalized requirement set and ask for confirmation if major assumptions, architecture decisions, priority boundaries, or scope boundaries remain uncertain.

Do not continue expanding scope after planning begins unless the user explicitly requests requirement changes. When the user adds or changes requirements after planning starts, pause planning, update the requirement set, identify the impact on design/tasks/risks, and re-freeze the requirements before continuing.

## Planning Output

After requirements are complete, choose an output structure based on task complexity. Do not force every section when the task is simple. Merge or omit sections when they do not add value.

For complex projects, use:

```markdown
## 需求概述

## 需求清单

## 优先级与范围

## 存疑点处理结果

## 方案边界与假设

## 总体设计

## 流程设计

## 类关系/模块关系

## 任务拆解

## 里程碑计划

## 验收标准

## 风险与应对
```

For small or medium tasks, use a lightweight structure:

```markdown
## 需求概述

## 范围与假设

## 任务拆解

## 验收标准

## 风险提示
```

Adjust section names to fit the user's domain, but preserve this order: requirements first, scope and assumptions second, design third, tasks fourth, validation and risks last.

## Mermaid Diagrams

Use Mermaid code blocks for design flows, class relationships, module relationships, state changes, sequence interactions, or deployment architecture when relevant.

Use diagrams only when they improve clarity. Avoid unnecessary diagrams for trivial logic or simple CRUD requirements. Prefer concise diagrams over large unreadable diagrams. Split complex workflows into multiple focused diagrams when necessary.

Choose diagram types by purpose:

- `flowchart TD` for business workflows, processing flows, and task pipelines.
- `sequenceDiagram` for interactions among users, services, and external systems.
- `classDiagram` for class, entity, domain model, or object relationships.
- `stateDiagram-v2` for lifecycle and status transitions.
- `erDiagram` for data entities and database relationships.

Example:

```mermaid
flowchart TD
    A[用户提交需求] --> B{需求是否完整}
    B -- 否 --> C[提出澄清问题]
    C --> A
    B -- 是 --> D[输出任务规划方案]
```

For class or module relationships, prefer a concise `classDiagram` or `flowchart` over prose-only explanations.

## Task Breakdown Rules

Make tasks atomic, executable, testable, dependency-aware, and traceable to requirements.

Each implementation task should ideally include:

- Objective: what the task accomplishes.
- Input/output: required inputs and expected outputs.
- Dependency: prerequisite requirements, designs, services, data, or decisions.
- Expected result: observable completion condition.
- Verification: how to test or review the result.

When the plan is large, group tasks by milestone or workstream, but keep each task small enough for a team member or agent to execute without rediscovering the requirement.

## Quality Bar

Make the final plan actionable and testable:

- Tie each task back to a requirement or acceptance criterion.
- Separate discovery, design, implementation, testing, deployment, and review tasks.
- Prioritize MVP and critical workflows before nice-to-have features.
- Include dependencies and ordering when they affect execution.
- Mark owners or roles when the user provides team information.
- Avoid over-planning details that the requirements do not justify.
- Use clear Chinese by default when the user writes in Chinese; otherwise match the user's language.
