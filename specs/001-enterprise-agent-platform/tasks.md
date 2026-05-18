# Tasks: 企业级通用多Agent数字员工平台

**Input**: [spec.md](./spec.md), [plan.md](./plan.md), [research.md](./research.md), [data-model.md](./data-model.md), [contracts/openapi.yaml](./contracts/openapi.yaml), [quickstart.md](./quickstart.md)  
**Generated**: 2026-05-18  
**Task Style**: Fine-grained, dependency-ordered, user-story organized  

## Summary

Total tasks: 210

Story task counts:

- US1 业务人员提交并跟踪数字员工任务: 31 tasks
- US2 管理员配置和发布数字员工: 24 tasks
- US3 审核人完成人工确认和责任留痕: 24 tasks
- US4 管理层评估试点效果和推广价值: 20 tasks
- US5 多场景验证平台通用能力: 28 tasks

MVP scope: Phase 1 + Phase 2 + US1.

## Format Rules

Every executable task follows:

```text
- [ ] [TaskID] [P?] [US?] Description with file path
```

No automated test tasks are included because TDD was not explicitly requested. Each story still includes independent acceptance criteria.

## Phase 1: Setup

**Purpose**: Create the TypeScript-first monorepo skeleton described in the implementation plan.

- [ ] T001 Create root package manifest with workspace definitions in package.json
- [ ] T002 Create shared TypeScript compiler configuration in tsconfig.base.json
- [ ] T003 Create root lint configuration for TypeScript packages in eslint.config.mjs
- [ ] T004 Create root formatting ignore rules in .prettierignore
- [ ] T005 Create environment variable template with no secrets in .env.example
- [ ] T006 Create API application package manifest in apps/api/package.json
- [ ] T007 Create API TypeScript configuration in apps/api/tsconfig.json
- [ ] T008 Create web console package manifest in apps/web-console/package.json
- [ ] T009 Create web console TypeScript configuration in apps/web-console/tsconfig.json
- [ ] T010 [P] Create domain package manifest in packages/domain/package.json
- [ ] T011 [P] Create workflow package manifest in packages/workflow/package.json
- [ ] T012 [P] Create access-control package manifest in packages/access-control/package.json
- [ ] T013 [P] Create audit package manifest in packages/audit/package.json
- [ ] T014 [P] Create integrations package manifest in packages/integrations/package.json
- [ ] T015 [P] Create agent-runtime package manifest in packages/agent-runtime/package.json
- [ ] T016 Add workspace scripts for typecheck, lint, build, and dev in package.json
- [ ] T017 Add application folder overview to repository README in README.md
- [ ] T018 Add local development notes for the generated workspace in docs/development.md

## Phase 2: Foundational

**Purpose**: Build shared primitives that every user story depends on.

- [ ] T019 Create shared entity identifier and timestamp types in packages/domain/src/shared/types.ts
- [ ] T020 [P] Create EnterpriseTenant domain type in packages/domain/src/tenant.ts
- [ ] T021 [P] Create User domain type in packages/domain/src/user.ts
- [ ] T022 [P] Create Department domain type in packages/domain/src/department.ts
- [ ] T023 [P] Create Project domain type in packages/domain/src/project.ts
- [ ] T024 [P] Create Role domain type in packages/domain/src/role.ts
- [ ] T025 [P] Create AccessScope domain type in packages/domain/src/access-scope.ts
- [ ] T026 [P] Create DigitalEmployee domain type in packages/domain/src/digital-employee.ts
- [ ] T027 [P] Create RoleConfiguration domain type in packages/domain/src/role-configuration.ts
- [ ] T028 [P] Create ProcessTemplate domain type in packages/domain/src/process-template.ts
- [ ] T029 [P] Create Task domain type and status enum in packages/domain/src/task.ts
- [ ] T030 [P] Create TaskStep domain type and status enum in packages/domain/src/task-step.ts
- [ ] T031 [P] Create Attachment domain type in packages/domain/src/attachment.ts
- [ ] T032 [P] Create KnowledgeSource domain type in packages/domain/src/knowledge-source.ts
- [ ] T033 [P] Create Citation domain type in packages/domain/src/citation.ts
- [ ] T034 [P] Create Rule domain type in packages/domain/src/rule.ts
- [ ] T035 [P] Create RuleResult domain type in packages/domain/src/rule-result.ts
- [ ] T036 [P] Create ReviewRecord domain type in packages/domain/src/review-record.ts
- [ ] T037 [P] Create OutputArtifact domain type in packages/domain/src/output-artifact.ts
- [ ] T038 [P] Create AuditRecord domain type in packages/domain/src/audit-record.ts
- [ ] T039 [P] Create ToolAdapter domain type in packages/domain/src/tool-adapter.ts
- [ ] T040 [P] Create OperationMetric domain type in packages/domain/src/operation-metric.ts
- [ ] T041 Export all domain entities from packages/domain/src/index.ts
- [ ] T042 Create repository interface base types in packages/domain/src/repositories/base-repository.ts
- [ ] T043 [P] Create TaskRepository interface in packages/domain/src/repositories/task-repository.ts
- [ ] T044 [P] Create DigitalEmployeeRepository interface in packages/domain/src/repositories/digital-employee-repository.ts
- [ ] T045 [P] Create ReviewRepository interface in packages/domain/src/repositories/review-repository.ts
- [ ] T046 [P] Create AuditRepository interface in packages/domain/src/repositories/audit-repository.ts
- [ ] T047 [P] Create KnowledgeRepository interface in packages/domain/src/repositories/knowledge-repository.ts
- [ ] T048 [P] Create OperationMetricRepository interface in packages/domain/src/repositories/operation-metric-repository.ts
- [ ] T049 Create request actor context type in packages/access-control/src/actor-context.ts
- [ ] T050 Create access decision result type in packages/access-control/src/access-decision.ts
- [ ] T051 Create access scope matcher for role + department/project + task range in packages/access-control/src/scope-matcher.ts
- [ ] T052 Create access guard function for task reads in packages/access-control/src/task-access.ts
- [ ] T053 Create access guard function for artifact reads in packages/access-control/src/artifact-access.ts
- [ ] T054 Create access guard function for audit queries in packages/access-control/src/audit-access.ts
- [ ] T055 Export access-control public API in packages/access-control/src/index.ts
- [ ] T056 Create audit event type constants in packages/audit/src/event-types.ts
- [ ] T057 Create audit writer interface in packages/audit/src/audit-writer.ts
- [ ] T058 Create audit retention helper for three-year minimum retention in packages/audit/src/retention.ts
- [ ] T059 Create workflow transition table for task states in packages/workflow/src/task-state-machine.ts
- [ ] T060 Create workflow transition table for task step states in packages/workflow/src/step-state-machine.ts
- [ ] T061 Create API server entrypoint in apps/api/src/server.ts
- [ ] T062 Create API route registration module in apps/api/src/routes/index.ts
- [ ] T063 Create API error response helper in apps/api/src/http/error-response.ts
- [ ] T064 Create OpenAPI contract copy under API app in apps/api/openapi.yaml
- [ ] T065 Create web console app shell in apps/web-console/src/app/App.tsx
- [ ] T066 Create web console route registry in apps/web-console/src/app/routes.tsx
- [ ] T067 Create API client base module in apps/web-console/src/api/client.ts
- [ ] T068 Create shared UI layout shell in apps/web-console/src/components/AppShell.tsx
- [ ] T069 Create seed data folder for the single enterprise pilot in apps/api/src/seeds/README.md
- [ ] T070 Create manual acceptance checklist folder in docs/acceptance/README.md

## Phase 3: User Story 1 - 业务人员提交并跟踪数字员工任务 (P1)

**Goal**: Business users can select a digital employee or task template, submit a task, track state, inspect intermediate results, and retrieve reviewed output.

**Independent Test Criteria**: A procurement, knowledge retrieval, or weekly report task can move from submission to a waiting-for-review state while the task board shows participating digital employees, current node, pending items, risk count, intermediate outputs, and estimated completion time.

- [ ] T071 [P] [US1] Create task create DTO aligned to OpenAPI TaskCreate in apps/api/src/modules/tasks/dto/task-create.dto.ts
- [ ] T072 [P] [US1] Create task summary DTO aligned to OpenAPI TaskSummary in apps/api/src/modules/tasks/dto/task-summary.dto.ts
- [ ] T073 [P] [US1] Create task detail DTO aligned to OpenAPI Task in apps/api/src/modules/tasks/dto/task-detail.dto.ts
- [ ] T074 [P] [US1] Create task step DTO aligned to OpenAPI TaskStep in apps/api/src/modules/tasks/dto/task-step.dto.ts
- [ ] T075 [P] [US1] Create output artifact DTO aligned to OpenAPI OutputArtifact in apps/api/src/modules/tasks/dto/output-artifact.dto.ts
- [ ] T076 [US1] Implement task creation validation rules in apps/api/src/modules/tasks/task-validation.ts
- [ ] T077 [US1] Implement task creation service with initial state submitted in apps/api/src/modules/tasks/task-create.service.ts
- [ ] T078 [US1] Implement default task step generation from process template in apps/api/src/modules/tasks/task-step-factory.ts
- [ ] T079 [US1] Implement task list query service with access-scope filtering in apps/api/src/modules/tasks/task-list.service.ts
- [ ] T080 [US1] Implement task detail query service with access-scope filtering in apps/api/src/modules/tasks/task-detail.service.ts
- [ ] T081 [US1] Implement task step query service in apps/api/src/modules/tasks/task-step.service.ts
- [ ] T082 [US1] Implement output artifact query service in apps/api/src/modules/tasks/output-artifact.service.ts
- [ ] T083 [US1] Add audit event writing for task_created in apps/api/src/modules/tasks/task-audit.ts
- [ ] T084 [US1] Add access_denied audit writing for rejected task reads in apps/api/src/modules/tasks/task-access-audit.ts
- [ ] T085 [US1] Add POST /tasks route handler in apps/api/src/modules/tasks/tasks.routes.ts
- [ ] T086 [US1] Add GET /tasks route handler in apps/api/src/modules/tasks/tasks.routes.ts
- [ ] T087 [US1] Add GET /tasks/{taskId} route handler in apps/api/src/modules/tasks/tasks.routes.ts
- [ ] T088 [US1] Add GET /tasks/{taskId}/steps route handler in apps/api/src/modules/tasks/tasks.routes.ts
- [ ] T089 [US1] Add GET /tasks/{taskId}/outputs route handler in apps/api/src/modules/tasks/tasks.routes.ts
- [ ] T090 [P] [US1] Create process template selector component in apps/web-console/src/features/tasks/ProcessTemplateSelect.tsx
- [ ] T091 [P] [US1] Create task expected output selector component in apps/web-console/src/features/tasks/ExpectedOutputSelect.tsx
- [ ] T092 [P] [US1] Create confidentiality level selector component in apps/web-console/src/features/tasks/ConfidentialitySelect.tsx
- [ ] T093 [P] [US1] Create task attachment picker shell in apps/web-console/src/features/tasks/AttachmentPicker.tsx
- [ ] T094 [US1] Create task submit form page in apps/web-console/src/features/tasks/TaskSubmitPage.tsx
- [ ] T095 [US1] Wire task submit form to POST /tasks in apps/web-console/src/features/tasks/useCreateTask.ts
- [ ] T096 [US1] Create task board list page in apps/web-console/src/features/tasks/TaskBoardPage.tsx
- [ ] T097 [P] [US1] Create task status badge component in apps/web-console/src/features/tasks/TaskStatusBadge.tsx
- [ ] T098 [P] [US1] Create task risk count indicator component in apps/web-console/src/features/tasks/RiskCountIndicator.tsx
- [ ] T099 [P] [US1] Create participating digital employees panel in apps/web-console/src/features/tasks/ParticipantPanel.tsx
- [ ] T100 [US1] Create task detail page with steps and outputs in apps/web-console/src/features/tasks/TaskDetailPage.tsx
- [ ] T101 [US1] Add US1 manual acceptance checklist in docs/acceptance/us1-task-submission-and-board.md

## Phase 4: User Story 2 - 管理员配置和发布数字员工 (P1)

**Goal**: Administrators can create, configure, evaluate, publish, suspend, or limit digital employees.

**Independent Test Criteria**: An administrator can create a lightweight digital employee with responsibilities, inputs, outputs, knowledge scope, tool permissions, prohibited actions, review points, evaluation samples, and pilot scope; eligible users can then see it in the catalog.

- [ ] T102 [P] [US2] Create digital employee create DTO in apps/api/src/modules/digital-employees/dto/digital-employee-create.dto.ts
- [ ] T103 [P] [US2] Create digital employee update DTO in apps/api/src/modules/digital-employees/dto/digital-employee-update.dto.ts
- [ ] T104 [P] [US2] Create digital employee response DTO in apps/api/src/modules/digital-employees/dto/digital-employee.dto.ts
- [ ] T105 [P] [US2] Create role configuration DTO in apps/api/src/modules/digital-employees/dto/role-configuration.dto.ts
- [ ] T106 [US2] Implement digital employee required-field validation in apps/api/src/modules/digital-employees/digital-employee-validation.ts
- [ ] T107 [US2] Implement prohibited-action defaulting for high-risk decisions and write-back actions in apps/api/src/modules/digital-employees/prohibited-action-policy.ts
- [ ] T108 [US2] Implement digital employee create service in apps/api/src/modules/digital-employees/digital-employee-create.service.ts
- [ ] T109 [US2] Implement digital employee update service in apps/api/src/modules/digital-employees/digital-employee-update.service.ts
- [ ] T110 [US2] Implement admission status transition service in apps/api/src/modules/digital-employees/admission-status.service.ts
- [ ] T111 [US2] Implement digital employee catalog query service with pilot-scope filtering in apps/api/src/modules/digital-employees/digital-employee-list.service.ts
- [ ] T112 [US2] Add audit event writing for digital employee create and update in apps/api/src/modules/digital-employees/digital-employee-audit.ts
- [ ] T113 [US2] Add GET /digital-employees route handler in apps/api/src/modules/digital-employees/digital-employees.routes.ts
- [ ] T114 [US2] Add POST /digital-employees route handler in apps/api/src/modules/digital-employees/digital-employees.routes.ts
- [ ] T115 [US2] Add GET /digital-employees/{digitalEmployeeId} route handler in apps/api/src/modules/digital-employees/digital-employees.routes.ts
- [ ] T116 [US2] Add PATCH /digital-employees/{digitalEmployeeId} route handler in apps/api/src/modules/digital-employees/digital-employees.routes.ts
- [ ] T117 [P] [US2] Create digital employee catalog page in apps/web-console/src/features/digital-employees/DigitalEmployeeCatalogPage.tsx
- [ ] T118 [P] [US2] Create digital employee role card component in apps/web-console/src/features/digital-employees/DigitalEmployeeCard.tsx
- [ ] T119 [P] [US2] Create role responsibilities editor in apps/web-console/src/features/digital-employees/ResponsibilitiesEditor.tsx
- [ ] T120 [P] [US2] Create prohibited actions editor in apps/web-console/src/features/digital-employees/ProhibitedActionsEditor.tsx
- [ ] T121 [P] [US2] Create knowledge scope selector in apps/web-console/src/features/digital-employees/KnowledgeScopeSelector.tsx
- [ ] T122 [P] [US2] Create tool permission selector in apps/web-console/src/features/digital-employees/ToolPermissionSelector.tsx
- [ ] T123 [P] [US2] Create review point editor in apps/web-console/src/features/digital-employees/ReviewPointEditor.tsx
- [ ] T124 [US2] Create digital employee configuration page in apps/web-console/src/features/digital-employees/DigitalEmployeeConfigPage.tsx
- [ ] T125 [US2] Add US2 manual acceptance checklist in docs/acceptance/us2-digital-employee-configuration.md

## Phase 5: User Story 3 - 审核人完成人工确认和责任留痕 (P1)

**Goal**: Reviewers can inspect outputs, citations, risk prompts, diffs, and submit approve/reject/request-changes decisions with responsibility traceability.

**Independent Test Criteria**: A pending output can be opened by an authorized reviewer, edited or commented, approved as final, and traced to reviewer, decision time, diff summary, citations, rule hits, and final artifact.

- [ ] T126 [P] [US3] Create review work item DTO in apps/api/src/modules/reviews/dto/review-work-item.dto.ts
- [ ] T127 [P] [US3] Create review submit DTO in apps/api/src/modules/reviews/dto/review-submit.dto.ts
- [ ] T128 [P] [US3] Create review record DTO in apps/api/src/modules/reviews/dto/review-record.dto.ts
- [ ] T129 [US3] Implement review assignment query service in apps/api/src/modules/reviews/review-work-item.service.ts
- [ ] T130 [US3] Implement review decision validation in apps/api/src/modules/reviews/review-validation.ts
- [ ] T131 [US3] Implement review submit service for approve, reject, and request_changes in apps/api/src/modules/reviews/review-submit.service.ts
- [ ] T132 [US3] Implement output finalization service that requires approval in apps/api/src/modules/reviews/output-finalization.service.ts
- [ ] T133 [US3] Implement artifact diff summary builder in apps/api/src/modules/reviews/artifact-diff.service.ts
- [ ] T134 [US3] Implement blocking rule result guard before approval in apps/api/src/modules/reviews/rule-blocking.guard.ts
- [ ] T135 [US3] Implement high-risk conclusion review guard in apps/api/src/modules/reviews/high-risk-review.guard.ts
- [ ] T136 [US3] Implement review audit writer for review_submitted and output_finalized in apps/api/src/modules/reviews/review-audit.ts
- [ ] T137 [US3] Add GET /reviews route handler in apps/api/src/modules/reviews/reviews.routes.ts
- [ ] T138 [US3] Add POST /tasks/{taskId}/reviews route handler in apps/api/src/modules/reviews/reviews.routes.ts
- [ ] T139 [P] [US3] Create review queue page in apps/web-console/src/features/reviews/ReviewQueuePage.tsx
- [ ] T140 [P] [US3] Create review output preview panel in apps/web-console/src/features/reviews/OutputPreviewPanel.tsx
- [ ] T141 [P] [US3] Create citation list panel in apps/web-console/src/features/reviews/CitationListPanel.tsx
- [ ] T142 [P] [US3] Create risk prompt panel in apps/web-console/src/features/reviews/RiskPromptPanel.tsx
- [ ] T143 [P] [US3] Create diff summary panel in apps/web-console/src/features/reviews/DiffSummaryPanel.tsx
- [ ] T144 [P] [US3] Create review decision form in apps/web-console/src/features/reviews/ReviewDecisionForm.tsx
- [ ] T145 [US3] Create review detail page in apps/web-console/src/features/reviews/ReviewDetailPage.tsx
- [ ] T146 [US3] Wire review decision form to POST /tasks/{taskId}/reviews in apps/web-console/src/features/reviews/useSubmitReview.ts
- [ ] T147 [US3] Add final artifact retention display to review detail page in apps/web-console/src/features/reviews/RetentionNotice.tsx
- [ ] T148 [US3] Add US3 manual acceptance checklist in docs/acceptance/us3-human-review-and-traceability.md
- [ ] T149 [US3] Document reviewer responsibility rules in docs/operations/reviewer-responsibility.md

## Phase 6: User Story 4 - 管理层评估试点效果和推广价值 (P2)

**Goal**: Operators and management can inspect and export task volume, success rate, adoption, processing time, modification rate, risk hit rate, saved effort, and feedback by task, digital employee, and scenario.

**Independent Test Criteria**: After pilot tasks exist, an operations owner can open the dashboard, filter by scenario/digital employee/time range, see all required metrics, and export a pilot report.

- [ ] T150 [P] [US4] Create operation metric query DTO in apps/api/src/modules/operations/dto/operation-metric-query.dto.ts
- [ ] T151 [P] [US4] Create operation metric response DTO in apps/api/src/modules/operations/dto/operation-metric.dto.ts
- [ ] T152 [US4] Implement task volume metric calculator in apps/api/src/modules/operations/metrics/task-volume.metric.ts
- [ ] T153 [US4] Implement success rate metric calculator in apps/api/src/modules/operations/metrics/success-rate.metric.ts
- [ ] T154 [US4] Implement adoption rate metric calculator in apps/api/src/modules/operations/metrics/adoption-rate.metric.ts
- [ ] T155 [US4] Implement average processing time metric calculator in apps/api/src/modules/operations/metrics/average-processing-time.metric.ts
- [ ] T156 [US4] Implement modification rate metric calculator in apps/api/src/modules/operations/metrics/modification-rate.metric.ts
- [ ] T157 [US4] Implement risk hit rate metric calculator in apps/api/src/modules/operations/metrics/risk-hit-rate.metric.ts
- [ ] T158 [US4] Implement saved effort metric calculator in apps/api/src/modules/operations/metrics/saved-effort.metric.ts
- [ ] T159 [US4] Implement user feedback metric calculator in apps/api/src/modules/operations/metrics/user-feedback.metric.ts
- [ ] T160 [US4] Implement operations metric query service with access-scope filtering in apps/api/src/modules/operations/operation-metric.service.ts
- [ ] T161 [US4] Add GET /operations/metrics route handler in apps/api/src/modules/operations/operations.routes.ts
- [ ] T162 [US4] Implement pilot report export service in apps/api/src/modules/operations/pilot-report-export.service.ts
- [ ] T163 [P] [US4] Create metric filter bar component in apps/web-console/src/features/operations/MetricFilterBar.tsx
- [ ] T164 [P] [US4] Create metric summary card component in apps/web-console/src/features/operations/MetricSummaryCard.tsx
- [ ] T165 [P] [US4] Create metric trend table component in apps/web-console/src/features/operations/MetricTrendTable.tsx
- [ ] T166 [P] [US4] Create pilot report export button in apps/web-console/src/features/operations/PilotReportExportButton.tsx
- [ ] T167 [US4] Create operations dashboard page in apps/web-console/src/features/operations/OperationsDashboardPage.tsx
- [ ] T168 [US4] Add US4 manual acceptance checklist in docs/acceptance/us4-operations-dashboard.md
- [ ] T169 [US4] Document metric definitions and formulas in docs/operations/metric-definitions.md

## Phase 7: User Story 5 - 多场景验证平台通用能力 (P2)

**Goal**: Procurement, knowledge retrieval, and project weekly report samples demonstrate that multiple scenarios reuse the same platform primitives.

**Independent Test Criteria**: Each sample scenario can be launched from a process template and produces its expected outputs, citations or risk prompts, review records, and audit trail without adding scenario-specific core platform logic.

- [ ] T170 [P] [US5] Create procurement process template seed in apps/api/src/seeds/process-templates/procurement.template.ts
- [ ] T171 [P] [US5] Create knowledge retrieval process template seed in apps/api/src/seeds/process-templates/knowledge-retrieval.template.ts
- [ ] T172 [P] [US5] Create project weekly report process template seed in apps/api/src/seeds/process-templates/project-weekly-report.template.ts
- [ ] T173 [P] [US5] Create procurement digital employee seed set in apps/api/src/seeds/digital-employees/procurement-employees.seed.ts
- [ ] T174 [P] [US5] Create knowledge retrieval digital employee seed set in apps/api/src/seeds/digital-employees/knowledge-employees.seed.ts
- [ ] T175 [P] [US5] Create project weekly report digital employee seed set in apps/api/src/seeds/digital-employees/project-report-employees.seed.ts
- [ ] T176 [P] [US5] Create sample policy knowledge source seed in apps/api/src/seeds/knowledge/policy-sources.seed.ts
- [ ] T177 [P] [US5] Create sample template knowledge source seed in apps/api/src/seeds/knowledge/template-sources.seed.ts
- [ ] T178 [P] [US5] Create sample historical case knowledge source seed in apps/api/src/seeds/knowledge/case-sources.seed.ts
- [ ] T179 [P] [US5] Create procurement output template definitions in apps/api/src/seeds/output-templates/procurement-output-templates.seed.ts
- [ ] T180 [P] [US5] Create knowledge retrieval output template definitions in apps/api/src/seeds/output-templates/knowledge-output-templates.seed.ts
- [ ] T181 [P] [US5] Create weekly report output template definitions in apps/api/src/seeds/output-templates/project-weekly-output-templates.seed.ts
- [ ] T182 [US5] Implement procurement sample flow assembler in apps/api/src/modules/sample-flows/procurement-flow.ts
- [ ] T183 [US5] Implement knowledge retrieval sample flow assembler in apps/api/src/modules/sample-flows/knowledge-retrieval-flow.ts
- [ ] T184 [US5] Implement project weekly report sample flow assembler in apps/api/src/modules/sample-flows/project-weekly-report-flow.ts
- [ ] T185 [US5] Implement sample citation generator for knowledge-backed outputs in apps/api/src/modules/sample-flows/sample-citation-generator.ts
- [ ] T186 [US5] Implement sample risk list generator for procurement and project flows in apps/api/src/modules/sample-flows/sample-risk-generator.ts
- [ ] T187 [US5] Implement sample artifact generator for procurement outputs in apps/api/src/modules/sample-flows/procurement-artifact-generator.ts
- [ ] T188 [US5] Implement sample artifact generator for knowledge retrieval outputs in apps/api/src/modules/sample-flows/knowledge-artifact-generator.ts
- [ ] T189 [US5] Implement sample artifact generator for project weekly report outputs in apps/api/src/modules/sample-flows/project-weekly-artifact-generator.ts
- [ ] T190 [P] [US5] Create scenario launcher page in apps/web-console/src/features/scenarios/ScenarioLauncherPage.tsx
- [ ] T191 [P] [US5] Create procurement scenario card in apps/web-console/src/features/scenarios/ProcurementScenarioCard.tsx
- [ ] T192 [P] [US5] Create knowledge retrieval scenario card in apps/web-console/src/features/scenarios/KnowledgeRetrievalScenarioCard.tsx
- [ ] T193 [P] [US5] Create project weekly report scenario card in apps/web-console/src/features/scenarios/ProjectWeeklyScenarioCard.tsx
- [ ] T194 [US5] Wire scenario cards to task submission defaults in apps/web-console/src/features/scenarios/useScenarioDefaults.ts
- [ ] T195 [US5] Create procurement sample verification guide in docs/scenarios/procurement.md
- [ ] T196 [US5] Create knowledge retrieval sample verification guide in docs/scenarios/knowledge-retrieval.md
- [ ] T197 [US5] Create project weekly report sample verification guide in docs/scenarios/project-weekly-report.md

## Phase 8: Polish & Cross-Cutting

**Purpose**: Tighten compliance, documentation, and acceptance readiness after the user stories are implemented.

- [ ] T198 Add no-business-system-write-back verification checklist in docs/acceptance/no-write-back.md
- [ ] T199 Add access-control verification checklist for role + department/project + task range in docs/acceptance/access-scope.md
- [ ] T200 Add three-year retention verification checklist in docs/acceptance/retention.md
- [ ] T201 Add pilot scale verification checklist for 200 users, 50 concurrent tasks, and 5,000 monthly tasks in docs/acceptance/pilot-scale.md
- [ ] T202 Add audit traceability verification checklist in docs/acceptance/audit-traceability.md
- [ ] T203 Update quickstart with application startup commands in specs/001-enterprise-agent-platform/quickstart.md
- [ ] T204 Update OpenAPI contract if implemented endpoints differ in specs/001-enterprise-agent-platform/contracts/openapi.yaml
- [ ] T205 Update data model with implementation field names in specs/001-enterprise-agent-platform/data-model.md
- [ ] T206 Update README with application run instructions in README.md
- [ ] T207 Add implementation notes for future Speckit analysis in specs/001-enterprise-agent-platform/implementation-notes.md
- [ ] T208 Review all documentation for terminology consistency in specs/001-enterprise-agent-platform/spec.md
- [ ] T209 Review all documentation for terminology consistency in specs/001-enterprise-agent-platform/plan.md
- [ ] T210 Review all documentation for terminology consistency in specs/001-enterprise-agent-platform/data-model.md

## Dependencies

### Phase Dependencies

- Phase 1 Setup must finish before Phase 2 Foundational.
- Phase 2 Foundational must finish before any user story phase.
- US1, US2, and US3 are all P1 and can be implemented after Phase 2; US1 is the suggested MVP.
- US4 depends on task, review, rule, and audit events from US1 and US3.
- US5 depends on task submission from US1, digital employee configuration from US2, review from US3, and operational samples from US4 only for richer reporting.
- Phase 8 Polish runs after all targeted stories for the release are complete.

### User Story Completion Order

1. US1 Business task submission and board
2. US2 Digital employee configuration
3. US3 Human review and traceability
4. US4 Operations dashboard
5. US5 Multi-scenario validation

### MVP Path

Complete T001-T070, then T071-T101. This produces the smallest independently demonstrable increment: a business user can submit and track a task.

## Parallel Execution Examples

### Setup

Run T010-T015 in parallel because each creates a different package manifest.

### Foundational

Run T020-T040 in parallel after T019 because each creates a separate domain entity file.

### US1

Run T090-T093 in parallel while backend tasks T076-T083 proceed, then integrate through T094-T100.

### US2

Run T117-T123 in parallel with backend service tasks T106-T112, then integrate through T124.

### US3

Run T139-T144 in parallel while backend review services T129-T136 proceed, then integrate through T145-T147.

### US4

Run T152-T159 in parallel because each metric calculator is isolated, then compose them through T160 and T167.

### US5

Run T170-T181 in parallel because each seed file or output template is independent, then implement flow assemblers T182-T184.

## Implementation Strategy

### MVP First

Build setup, shared domain, access control, audit primitives, and US1. Keep data in a simple repository adapter until the first end-to-end task flow is visible.

### Incremental Delivery

After US1, add US2 so administrators can configure digital employees. Add US3 to close the human accountability loop. Add US4 and US5 once real task, review, and audit events exist.

### Compliance Guardrails

Do not implement any endpoint, adapter, UI action, or workflow transition that writes back to customer business systems in Phase 1. Every sensitive read or detail view must pass role + department/project + task range checks and write an audit event for denied access.
