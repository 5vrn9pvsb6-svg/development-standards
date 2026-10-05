# Project Requirements

English translation | [Chinese template source](../zh-CN/requirements-template.md) | Paired revision: `2026-10-05.9`

Applicability: use when formal development requires a requirements document. Qualifying low-risk localized repairs or behavior-preserving refactors do not require copying/filling this template because historical documents are absent. Update relevant existing records when necessary; scope/risk increases use the formal process.

Usage: preserve repository formats. Record actual discussion results, remove irrelevant sections, and explain consequential non-applicable items. Put unsupported information in open questions, not "approved" by default. Adapt numbering to the project.

## Document State and Scope

- Document identity/path and current content version; project/feature and related records.
- Applicable scope: current requirement IDs, feature boundaries, main non-goals. Distinguish approved/pending scopes under partial approval; do not mark the whole document approved.
- Actual state: draft, pending approval, approved, or reapproval required.
- Approval: approved content version/scope and authentic verifiable user feedback or project record. Without it, mark unapproved; do not invent message IDs.
- Open issues: link the question table below and identify blockers for this scope.
- Reapproval triggers: material requirements/acceptance or permission/data changes; record affected prior versions/scope.

Status labels or versions alone do not prove approval. Formatting, spelling, and business-preserving evidence updates do not automatically invalidate approval. Business changes invalidate affected requirements and dependent design approvals.

## Goals and Scenarios

Describe target users, the problem, current situation, and intended results. List main flows/roles; distinguish business objectives from technical solutions.

## Scope and Non-Goals

List included/excluded capabilities and existing behavior that must remain unchanged. Future plans are not current acceptance scope.

## Functional Requirements and Business Rules

Use one actual record per requirement; add sections for complex rules when needed.

| Requirement ID | Scenario and intended behavior | Inputs/outputs and rules | Boundaries/failures | Acceptance criteria |
| --- | --- | --- | --- | --- |

Acceptance states conditions, actions, and observable results, not just "works" or "good experience." Reuse existing acceptance IDs and tests.

## Constraints and Non-Functional Requirements

Fill only relevant topics: permissions/data ownership, privacy/security, compatibility, external dependencies, environment, performance/capacity/availability. Mark undecided metrics pending confirmation rather than inventing them.

### Stack Constraints and Preferences (Especially New Projects)

Record platform, deployment environment, budget/resource constraints, maintainers/capacity, integrations, user-specified technology, and acceptable trade-offs. Non-technical users can express "easy to deploy" or "manageable costs" without choosing frameworks upfront. Mark unknowns pending; do not invent budgets or schedules.

This section records constraints/preferences, not model recommendations as user decisions. Discuss stack options after requirements approval and record the choice/authentic source in architecture; no separate stack document is required.

### Older-Agent Compatibility (Only for Client/Server Communication)

Record older-Agent version scope and user/project basis, protocol/interface/field-semantic baselines, required core flows, and acceptance. Agent is a product client/collector, not an AI agent. Unclear scope is an open issue; do not invent minimum versions or exclude older versions.

Server upgrades must not force Agent upgrades for existing workflows to keep operating. Breaking changes must not be merged/released. Agent-interaction changes require corresponding older-version evidence; failure, necessary checks not run, or missing evidence block merge/release. Without such communication, mark not applicable rather than invent a matrix.

## Assumptions, Open Questions, and Conclusions

Distinguish approved facts, assumptions to verify, and user choices.

| Question/assumption | Design/implementation impact | Blocks current scope? | User conclusion or next action |
| --- | --- | --- | --- |

## Requirements Change Record

Record material changes, affected requirement IDs/acceptance, and whether renewed approval is needed. Modification time is not an approval record.
