# Research: 企业级通用多Agent数字员工平台

## Decision: Use a TypeScript-first modular web platform

**Rationale**: The current repository already contains JavaScript-based document generation, and the product needs both a browser console and a service layer. A TypeScript-first approach keeps frontend, API contracts, domain types, and workflow logic aligned while still allowing existing JavaScript assets to remain.

**Alternatives considered**:

- Java/Spring-style enterprise backend: strong for enterprise systems, but heavier for an MVP and less aligned with the current repo.
- Python-first backend: convenient for AI workflows, but would split web/domain typing unless additional tooling is introduced.

## Decision: Use REST contracts for Phase 1

**Rationale**: The Phase 1 user actions map cleanly to resources: digital employees, tasks, task steps, reviews, audit records, outputs, and metrics. REST is easier for customer IT teams to inspect, mock, and integrate during a pilot.

**Alternatives considered**:

- GraphQL: flexible for dashboards, but increases schema governance and permission complexity early.
- Event-only contracts: useful internally, but not sufficient as a customer-facing integration and testing contract.

## Decision: Model work as durable tasks with explicit state transitions

**Rationale**: The core product promise is trackable multi-Agent work with human review, rollback, and audit. Explicit task and step states make task boards, review workbenches, retries, and audit traceability testable.

**Alternatives considered**:

- Chat-session model: simpler to start, but does not support multi-role state, review gates, or operational reporting well.
- Fully autonomous process execution: conflicts with the Phase 1 human accountability boundary.

## Decision: Implement a tool gateway with read-only/export/notification/todo adapters only

**Rationale**: The clarified scope forbids write-back to business systems. A gateway still centralizes authorization, logging, adapter configuration, and future extension while ensuring Phase 1 actions stay inside allowed boundaries.

**Alternatives considered**:

- Direct system integration from each digital employee: faster for demos, but weak for audit and permission control.
- Immediate low-risk write-back: deferred because the clarified boundary explicitly excludes all business-system write-back.

## Decision: Use role + department/project + task range as the minimum access model

**Rationale**: Role-only access is too coarse for multi-department enterprise pilots. The clarified access scope is specific enough to drive data modeling, acceptance tests, and audit behavior without requiring full customer IAM synchronization in Phase 1.

**Alternatives considered**:

- Role-only permissions: lower implementation effort, but insufficient for cross-department tasks and audit views.
- Data classification plus role/department/project/task: stronger, but the clarified minimum does not require it for Phase 1.

## Decision: Store citation metadata for all knowledge-backed outputs

**Rationale**: The spec requires at least 85% of knowledge or policy outputs to include auditable source references. Citation metadata should include source identity, title, version, applicability, excerpt or locator, and retrieval time.

**Alternatives considered**:

- Free-text citations only: hard to validate and difficult to audit.
- No citation model until later: would undercut review quality and traceability success criteria.

## Decision: Treat audit records and final outputs as retention-managed records

**Rationale**: The clarified requirement sets a 3-year minimum. Retention metadata should be explicit on audit records and final output artifacts so compliance queries can verify retention coverage.

**Alternatives considered**:

- Global retention setting only: simpler, but weaker for proof at record level.
- Customer-defined retention only: useful later, but Phase 1 needs a measurable baseline.

## Decision: Keep operational metrics derived from task, review, rule, and audit events

**Rationale**: Metrics such as success rate, adoption, modification rate, risk hits, and saved effort should reconcile to task history and audit events. This avoids a separate metrics truth source during the pilot.

**Alternatives considered**:

- Manual reporting spreadsheet: acceptable for early sales demos, but weak for ongoing operation.
- Separate analytics-only event stream from day one: useful at scale, but unnecessary for 5,000 tasks per month in Phase 1.

## Decision: Use sample flows for procurement, knowledge retrieval, and project weekly reports

**Rationale**: These scenarios jointly validate complex workflows, citation quality, rule checks, human review, and reporting. They also prove that the same platform primitives can serve multiple business contexts.

**Alternatives considered**:

- Procurement only: validates compliance-heavy workflow but not broad platform reuse.
- Knowledge retrieval only: validates citations but not multi-step process orchestration.
