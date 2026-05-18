# Implementation Plan: 企业级通用多Agent数字员工平台

**Branch**: `main`  
**Spec**: [spec.md](./spec.md)  
**Created**: 2026-05-18  
**Plan Status**: Ready for task generation  

## Setup Notes

The repository does not currently contain the standard Spec Kit scaffold:

- Missing `.specify/scripts/bash/setup-plan.sh`
- Missing `.specify/memory/constitution.md`
- Missing `.specify/templates/plan-template.md`
- Missing `.specify/scripts/bash/update-agent-context.sh`

This plan therefore follows the Spec Kit plan workflow manually and records generated artifacts in the expected feature directory. No unresolved `NEEDS CLARIFICATION` items remain in the feature spec.

## Technical Context

**Language/Runtime**: TypeScript for application code, with the current JavaScript document-generation script retained as a supporting artifact.  
**Frontend**: Web console for business users, reviewers, administrators, and operators.  
**Backend**: Modular service layer exposing REST contracts and coordinating workflows, permissions, audit, and integrations.  
**Workflow Model**: Durable task workflow with explicit task states, step states, review gates, and rollback/retry paths.  
**Data Storage**: Relational store for business entities and state; object storage for attachments and output artifacts; search index/vector-capable knowledge index for enterprise knowledge retrieval.  
**Async Processing**: Background job queue for agent execution, document processing, rule checks, artifact generation, and metrics aggregation.  
**AI/Agent Layer**: Agent runtime behind a model gateway, with all tool use mediated by the platform tool gateway.  
**Integration Boundary**: Read-only queries, export, message notification, and todo push only. No business-system write-back in Phase 1.  
**Security Boundary**: Single enterprise tenant; minimum access scope is role + department/project + task range.  
**Retention**: Audit records and final output artifacts must be retained for at least 3 years.  
**Scale Baseline**: 200 pilot users, 50 concurrent tasks, 5,000 tasks per month.  

## Constitution Check

No formal project constitution file is present. The following gates are derived from the feature spec and local workflow rules:

- **User value first**: All work must map to task submission, digital employee configuration, human review, audit, or operational visibility.
- **Human accountability**: High-risk conclusions must never bypass authorized human review.
- **No write-back**: Phase 1 must not write any formal, draft, remark, or status field back to business systems.
- **Least privilege**: Every data access and tool action must be scoped by role + department/project + task range.
- **Traceability**: Final outputs must be traceable to inputs, knowledge sources, agent outputs, rule hits, human edits, and final approval.
- **Cross-scenario reuse**: Procurement, knowledge retrieval, and weekly project report scenarios must reuse the same platform primitives.

**Initial Gate Result**: PASS. The plan keeps the implementation inside the clarified Phase 1 boundaries.

## Project Structure

```text
specs/001-enterprise-agent-platform/
├── spec.md
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
└── contracts/
    └── openapi.yaml
```

Suggested future application layout:

```text
apps/
├── web-console/
└── api/
packages/
├── domain/
├── workflow/
├── agent-runtime/
├── access-control/
├── audit/
└── integrations/
```

## Phase 0: Research

Research decisions are captured in [research.md](./research.md). Key resolved choices:

- TypeScript-first modular web platform
- REST API contract for Phase 1
- Durable task workflow with explicit review gates
- Tool gateway with read-only and notification/export adapters only
- Attribute-based access checks using role + department/project + task range
- 3-year audit and output artifact retention metadata

## Phase 1: Design & Contracts

Design artifacts generated:

- [data-model.md](./data-model.md): domain entities, relationships, validation rules, and lifecycle transitions
- [contracts/openapi.yaml](./contracts/openapi.yaml): REST API contract covering user actions and operational flows
- [quickstart.md](./quickstart.md): local validation and planning handoff guide

Agent context update:

- The standard `.specify/scripts/bash/update-agent-context.sh` script is absent.
- A lightweight project `AGENTS.md` has been created to persist Speckit workflow reminders and the plan-level technical context for Codex.

## Phase 2: Task Planning Preview

The next `speckit-tasks` phase should split work in this order:

1. Repository scaffold and shared domain model
2. Access scope and identity model
3. Digital employee catalog and role configuration
4. Task submission and task board
5. Workflow state machine and step execution
6. Knowledge source registration and citation handling
7. Tool gateway with read-only/query/export/notification/todo adapters
8. Rule checks and risk list generation
9. Human review workbench and version comparison
10. Audit trail, retention metadata, and searchable audit views
11. Operational metrics and pilot reporting
12. Procurement, knowledge retrieval, and project weekly report sample flows
13. End-to-end acceptance tests against clarified success criteria

## Post-Design Constitution Check

**Result**: PASS.

- The design preserves the single-enterprise tenant boundary.
- No API contract exposes business-system write-back.
- All sensitive access paths include an access-scope concept.
- Audit and output retention are represented explicitly.
- The data model supports cross-scenario reuse through generic tasks, process templates, digital employees, rules, knowledge sources, outputs, reviews, and audit records.

## Risks & Mitigations

- **Missing full Spec Kit scaffold**: Keep generated artifacts in the expected paths and note the script gap. Add `.specify/` later if the team wants strict tool compatibility.
- **Integration uncertainty**: Use read-only adapters and simulated business data until customer systems are available.
- **Knowledge quality variance**: Require source version, applicability, and citation metadata before outputs can be approved.
- **Permission gaps**: Implement access scope checks before any task, artifact, audit, or operational detail view.
- **Agent output uncertainty**: Keep rule checks and human review mandatory for final outputs.

## Next Step

Run `speckit-tasks` to generate implementation tasks from these planning artifacts.
