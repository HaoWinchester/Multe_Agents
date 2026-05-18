# Personal Workflow Reminders

## Speckit Order

When working on this repository with Speckit, use this default order:

```text
speckit-constitution   optional, for initial project principles/governance
speckit-specify        create spec.md from natural-language requirements
speckit-clarify        optional but recommended before planning
speckit-plan           create plan.md and design artifacts
speckit-tasks          create dependency-ordered tasks.md
speckit-analyze        optional read-only consistency check before implementation
speckit-checklist      optional extra requirements-quality gate
speckit-implement      implement tasks and mark completed tasks in tasks.md
```

Use this compact daily flow unless a special path is requested:

```text
specify -> clarify -> plan -> tasks -> analyze -> implement
```

Special Speckit paths:

- Use `speckit-baseline` instead of `speckit-specify` when deriving a spec from existing or legacy code.
- Use `speckit-taskstoissues` after `speckit-tasks` when GitHub issues should be generated from `tasks.md`.

## Current Feature Context

- Feature directory: `specs/001-enterprise-agent-platform/`
- Spec: `specs/001-enterprise-agent-platform/spec.md`
- Plan: `specs/001-enterprise-agent-platform/plan.md`
- Contracts: `specs/001-enterprise-agent-platform/contracts/openapi.yaml`

Key clarified Phase 1 boundaries:

- Single enterprise tenant pilot
- Audit records and final output artifacts retained for at least 3 years
- Integration actions limited to read-only query, export, message notification, and todo push
- No business-system write-back
- Minimum access control grain: role + department/project + task range
- Pilot capacity baseline: 200 users, 50 concurrent tasks, 5,000 tasks/month

## Technical Direction

- TypeScript-first modular web platform
- REST contracts for Phase 1
- Durable task workflow with human review gates
- Tool gateway mediates all system/tool access
- Audit trail is a first-class domain model
- Procurement, knowledge retrieval, and project weekly report flows should reuse shared platform primitives
