# Data Model: 企业级通用多Agent数字员工平台

## Entity Overview

### EnterpriseTenant

Represents the single enterprise pilot boundary.

**Fields**:

- `id`: unique tenant identifier
- `name`: enterprise display name
- `status`: active, suspended
- `retention_policy_years`: minimum 3 for Phase 1
- `created_at`, `updated_at`

**Relationships**:

- Has many users, departments, projects, digital employees, process templates, tasks, knowledge sources, rules, and audit records.

### User

Represents a person using the platform.

**Fields**:

- `id`
- `tenant_id`
- `display_name`
- `email`
- `status`: active, disabled
- `primary_department_id`
- `role_assignments`
- `created_at`, `updated_at`

**Validation Rules**:

- User must belong to the single enterprise tenant.
- Disabled users cannot initiate tasks, review outputs, or view restricted records.

### Department

Represents an enterprise department used for access scoping.

**Fields**:

- `id`
- `tenant_id`
- `name`
- `parent_department_id`
- `status`

### Project

Represents a project or business workstream used for access scoping.

**Fields**:

- `id`
- `tenant_id`
- `name`
- `owning_department_id`
- `status`: active, archived

### Role

Represents platform roles.

**Fields**:

- `id`
- `name`: business_user, reviewer, digital_employee_admin, operations_owner, auditor, security_admin
- `description`
- `permissions`

**Validation Rules**:

- Role alone is insufficient for sensitive access; it must be combined with department/project and task range.

### AccessScope

Represents the minimum authorization boundary.

**Fields**:

- `id`
- `tenant_id`
- `subject_type`: user, digital_employee
- `subject_id`
- `role_id`
- `department_ids`
- `project_ids`
- `task_scope`: own_tasks, department_project_tasks, assigned_review_tasks, audit_scope
- `valid_from`, `valid_until`

**Validation Rules**:

- Access decisions for task submission, artifact viewing, review actions, audit querying, and operational detail views must evaluate role + department/project + task range.

### DigitalEmployee

A business-recognizable digital role.

**Fields**:

- `id`
- `tenant_id`
- `name`
- `description`
- `responsibilities`
- `prohibited_actions`
- `input_requirements`
- `output_types`
- `status`: draft, in_evaluation, pilot, active, suspended, retired
- `evaluation_metrics`
- `created_by`, `created_at`, `updated_at`

**Relationships**:

- Has one or more role configurations.
- Can participate in many process templates and tasks.

### RoleConfiguration

Admin-maintained configuration for a digital employee.

**Fields**:

- `id`
- `digital_employee_id`
- `version`
- `knowledge_scope_ids`
- `tool_permission_ids`
- `output_template_ids`
- `review_points`
- `risk_boundaries`
- `pilot_scope`
- `admission_status`: not_ready, ready_for_pilot, approved, suspended
- `effective_from`, `effective_until`

**Validation Rules**:

- A digital employee cannot be used in a formal pilot task unless its configuration is ready for pilot or approved.
- Prohibited actions must include high-risk final decisions and all business-system write-back actions in Phase 1.

### ProcessTemplate

Reusable workflow template.

**Fields**:

- `id`
- `tenant_id`
- `name`
- `scenario_type`: procurement, knowledge_retrieval, project_weekly_report, generic
- `description`
- `steps`
- `review_gate_definitions`
- `rollback_rules`
- `status`: draft, pilot, active, retired

### Task

Business work request submitted by a user.

**Fields**:

- `id`
- `tenant_id`
- `process_template_id`
- `submitted_by`
- `business_type`
- `natural_language_request`
- `confidentiality_level`
- `expected_outputs`
- `department_id`
- `project_id`
- `status`: draft, submitted, collecting_inputs, running, waiting_for_review, changes_requested, approved, archived, cancelled, failed
- `estimated_completion_time`
- `created_at`, `updated_at`, `completed_at`

**Relationships**:

- Has many task steps, attachments, output artifacts, review records, rule results, audit records, and operation metrics.

**State Transitions**:

- draft -> submitted
- submitted -> collecting_inputs
- collecting_inputs -> running
- running -> waiting_for_review
- waiting_for_review -> changes_requested
- changes_requested -> running
- waiting_for_review -> approved
- approved -> archived
- any active state -> cancelled or failed

### TaskStep

Trackable unit within a task.

**Fields**:

- `id`
- `task_id`
- `step_type`: input_collection, knowledge_retrieval, agent_generation, rule_check, human_review, export, archive, metrics_update
- `assigned_digital_employee_id`
- `status`: pending, running, blocked, completed, failed, skipped
- `started_at`, `completed_at`
- `summary`
- `error_message`

### Attachment

User-provided or system-imported task material.

**Fields**:

- `id`
- `task_id`
- `file_name`
- `content_type`
- `storage_uri`
- `confidentiality_level`
- `uploaded_by`
- `created_at`

### KnowledgeSource

Authorized knowledge or document source.

**Fields**:

- `id`
- `tenant_id`
- `name`
- `source_type`: policy, template, historical_case, field_dictionary, business_document
- `version`
- `applicability_scope`
- `owner_department_id`
- `access_scope`
- `status`: active, archived

### Citation

Reference metadata attached to generated outputs.

**Fields**:

- `id`
- `task_id`
- `output_artifact_id`
- `knowledge_source_id`
- `source_title`
- `source_version`
- `locator`
- `applicability_note`
- `retrieved_at`

**Validation Rules**:

- Knowledge-backed answers and policy-backed outputs should include citation metadata unless the reviewer explicitly marks the source unavailable.

### Rule

Business, quality, permission, or risk rule.

**Fields**:

- `id`
- `tenant_id`
- `name`
- `rule_type`: format, field_completeness, permission, policy, risk, quality
- `severity`: info, warning, blocking
- `status`: draft, active, retired
- `owner`

### RuleResult

Result of a rule check for a task or output.

**Fields**:

- `id`
- `task_id`
- `rule_id`
- `target_type`: task, task_step, output_artifact
- `target_id`
- `result`: pass, warning, fail
- `message`
- `created_at`

**Validation Rules**:

- Blocking failures prevent final approval until resolved or explicitly overridden by an authorized reviewer.

### ReviewRecord

Human review and responsibility record.

**Fields**:

- `id`
- `task_id`
- `output_artifact_id`
- `reviewer_id`
- `decision`: approve, reject, request_changes
- `comments`
- `diff_summary`
- `created_at`

**Validation Rules**:

- Final output artifacts require an approving review record.
- High-risk conclusions cannot become final without authorized review.

### OutputArtifact

Intermediate or final task output.

**Fields**:

- `id`
- `task_id`
- `artifact_type`: requirement_form, procurement_list, tender_draft, risk_list, cited_answer, project_weekly_report, todo_tracking_sheet, audit_ledger, generic_document
- `title`
- `status`: draft, pending_review, final, archived, rejected
- `storage_uri`
- `created_by_type`: user, digital_employee, system
- `created_by_id`
- `finalized_by`
- `finalized_at`
- `retention_until`

**Validation Rules**:

- Final artifacts must have review approval and retention metadata.
- Retention must be at least 3 years from finalization for Phase 1.

### AuditRecord

Immutable task trace entry.

**Fields**:

- `id`
- `tenant_id`
- `task_id`
- `actor_type`: user, digital_employee, system
- `actor_id`
- `event_type`: task_created, access_allowed, access_denied, knowledge_retrieved, tool_called, agent_output_generated, rule_hit, review_submitted, output_finalized, export_generated, notification_sent
- `event_summary`
- `related_entity_type`
- `related_entity_id`
- `timestamp`
- `retention_until`

**Validation Rules**:

- Access denied events must be recorded.
- Audit records must be retained for at least 3 years.

### ToolAdapter

Represents a tool or integration capability.

**Fields**:

- `id`
- `tenant_id`
- `name`
- `adapter_type`: identity, document, message, todo, read_only_business_source, export
- `allowed_actions`: query, export, notify, create_todo
- `status`: configured, disabled

**Validation Rules**:

- Phase 1 adapters must not expose any write-back actions to business systems.

### OperationMetric

Metric derived from task and audit events.

**Fields**:

- `id`
- `tenant_id`
- `metric_type`: task_volume, success_rate, adoption_rate, average_processing_time, modification_rate, risk_hit_rate, saved_effort, user_feedback
- `dimension_type`: task, digital_employee, scenario, department, project
- `dimension_id`
- `period_start`
- `period_end`
- `value`

## Scenario-Specific Outputs

### Procurement

- Requirement form
- Centralized procurement list
- Tender draft
- Risk list
- Archive directory or audit ledger

### Knowledge Retrieval

- Cited answer
- Similar cases
- Template recommendation
- Access log

### Project Weekly Report

- Weekly report
- Risk list
- Todo tracking sheet

## Cross-Cutting Validation

- Every task belongs to the single enterprise tenant.
- Every sensitive read checks access scope.
- Every tool call is recorded in audit records.
- Every final output is linked to task input, citations, rule results, review records, and retention metadata.
- No Phase 1 adapter may write back to a business system.
