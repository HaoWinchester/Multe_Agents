# Quickstart: 企业级通用多Agent数字员工平台

This repository currently contains planning artifacts rather than an application implementation. Use this guide to validate the planning package and hand it into the next Speckit phase.

## 1. Review Source Inputs

```bash
open "企业级通用多Agent系统可行性及落地方案.docx"
sed -n '1,240p' specs/001-enterprise-agent-platform/spec.md
```

Confirm the clarified Phase 1 boundaries:

- Single enterprise tenant
- 3-year minimum retention for final outputs and audit records
- Read-only query, export, message notification, and todo push only
- Access scope = role + department/project + task range
- Pilot scale = 200 users, 50 concurrent tasks, 5,000 tasks/month

## 2. Validate Planning Artifacts

```bash
ls -la specs/001-enterprise-agent-platform
ls -la specs/001-enterprise-agent-platform/contracts
```

Expected files:

- `plan.md`
- `research.md`
- `data-model.md`
- `contracts/openapi.yaml`
- `quickstart.md`

## 3. Inspect API Contract

```bash
sed -n '1,260p' specs/001-enterprise-agent-platform/contracts/openapi.yaml
```

Check that the contract includes:

- Digital employee catalog and configuration
- Task submission and task board
- Task outputs and exports
- Human review submission
- Knowledge source and citation queries
- Audit record search
- Operational metrics
- Notification/todo push only

The contract must not expose any endpoint that writes formal, draft, remark, or status fields back to customer business systems.

## 4. Validate Data Model Coverage

```bash
sed -n '1,260p' specs/001-enterprise-agent-platform/data-model.md
```

Trace each success criterion to model support:

- Task lifecycle supports end-to-end task closure.
- Output artifacts and audit records include retention metadata.
- AccessScope models role + department/project + task range.
- ReviewRecord anchors human accountability.
- ToolAdapter excludes write-back actions.
- OperationMetric supports pilot reporting.

## 5. Suggested Local Smoke Checks

```bash
rg -n "NEEDS CLARIFICATION|TODO|TBD" specs/001-enterprise-agent-platform || true
rg -n "write-back|写回" specs/001-enterprise-agent-platform
rg -n "3 年|retention|retentionUntil" specs/001-enterprise-agent-platform
```

Expected result:

- No unresolved clarification markers.
- Any write-back references should forbid business-system write-back.
- Retention appears in spec, data model, and contract.

## 6. Next Speckit Step

Run `speckit-tasks` next. The task generation should consume:

- [spec.md](./spec.md)
- [plan.md](./plan.md)
- [research.md](./research.md)
- [data-model.md](./data-model.md)
- [contracts/openapi.yaml](./contracts/openapi.yaml)

Recommended task ordering is listed in the Phase 2 preview section of [plan.md](./plan.md).
