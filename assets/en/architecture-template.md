# Modules and Architecture

English translation | [Chinese template source](../zh-CN/architecture-template.md) | Paired revision: `2026-10-05.9`

Applicability: use when formal development requires an architecture document. Qualifying low-risk localized repairs or behavior-preserving refactors do not require copying/filling this template because historical documents are absent. Update relevant existing records when necessary; scope/risk increases use the formal process.

Usage: discuss and fill based on approved requirements; reuse existing designs. Adjust depth to scale. Do not add layers/services/technologies merely to fill the template. Mark nonexistent paths as planned.

## Document State and Design Basis

- Identity/path, current design content version, module/requirement scope and necessary dependencies. Distinguish approved/pending scopes under partial approval.
- Design basis: corresponding requirements identity, version, approved scope.
- Actual state: draft, pending approval, approved, or reapproval required.
- Approval: approved version/scope and authentic verifiable user feedback or project source; otherwise mark unapproved.
- Open issues and implementation blockers; reapproval triggers such as material underlying requirements, stack, interfaces, responsibilities, or dependency direction changes.

A file's "approved" claim grants no authority. Design content and approval metadata/implementation evidence can be separate; adding actual code/test evidence without changing design does not require reapproval.

## Stack Options and Confirmation

For new projects with approved requirements, normally offer 2-3 viable options, mark a recommendation, and explain delivery, deployment, maintenance, scalability, and risk plainly. Preserve user-specified choices; explain when one option fits rather than invent alternatives. Existing projects may link an approved stack baseline without reselection.

| Option and rationale | Plain explanation and fit | Technologies | Cost, deployment, maintenance | Scalability, limits, risk |
| --- | --- | --- | --- | --- |

Record selected main language/runtime, client/frontend, server, storage, build/tests, and deployment as applicable. Include versions/compatibility ranges, rationale, and unverified issues without unnecessary components. Costs/schedules without evidence are estimates or unknowns.

- Actual choice status: to discuss, pending approval, approved, or reapproval required.
- Authentic source/scope: explicit choice or approval of an architecture clearly stating the stack; tie to this version. A request for recommendations is not approval; do not invent it.
- Open issues, verification, blockers, material stack-change impact, renewed approvals.

Stack approval alone neither approves requirements/complete architecture for the current implementation scope nor authorizes formal scaffolding/implementation. Unresolved alternatives are not final choices. Link current design-scope approval where applicable rather than duplicate ledgers.

## Visual Alternatives and User Selection (When Interface Design Applies)

Under the [engineering workflow](../../references/en/engineering-workflow.md), provide three meaningfully distinct HTML visual prototypes/mockup pages using the same requirements, representative screens, sample data, and viewports within project brand/design constraints, prioritizing aesthetics, layout, color, typography, and hierarchy. Each needs a browser-openable entry and actual rendering-check results. Static HTML/CSS is sufficient; JS/interactions are optional by default, without complete business flows. Add scoped demos only when explicitly requested. Text-only options, empty placeholders, or color swaps are insufficient; images supplement but cannot replace HTML entries. Link valid applicable existing selections for reuse; without a UI, mark not applicable without empty options.

| Option | Version/scope and HTML entry | Layout/visual differences | Display scope, rendering checks, and trade-offs |
| --- | --- | --- | --- |
| A | | | |
| B | | | |
| C | | | |

Record recommendation rationale, actual selected/pending state, authentic source, option version/scope, and any combined revision preview. Selection can accompany this document's approval without a separate ledger. Missing previews are not shown; do not implement unsettled UI before selection or treat selection as full architecture approval. Implementing/repairing established design does not force reselection; actual redesign applies to current scope.

## System Boundary and Overall Structure

Describe internals, users/roles, dependencies, and runtime boundary. List actual frameworks/infrastructure and rationale, not microservices by default. Complex modules require an architecture diagram here or in the relevant module section, showing internal components, boundaries, dependency/data-flow directions, and key external participants consistent with module-table nodes/edges. It is not an optional illustration. Criteria/formats are in the [engineering workflow](../../references/en/engineering-workflow.md).

## Module Responsibilities and Code Ownership

Divide by business responsibility with explicit interfaces/allowed dependencies; modules are not each file/function.

| Module ID/name | Responsibilities | Non-responsibilities | Existing/planned paths | Public interfaces | Allowed dependencies |
| --- | --- | --- | --- | --- | --- |

Explain avoidance of cycles, cross-layer access, and duplicated rules. Do not create synonymous modules when existing ones suffice.

## Key Flows and Collaboration

For important scenarios, describe entrypoints, call order, data flow, results, and errors. Async/external calls cover triggers, completion, and failure. Complex workflows require flowcharts covering decisions/branches, owning modules, termination/results, and key failure paths, with actual concurrency, retries, or compensation as applicable. Sequence/state diagrams may supplement but not replace required flowcharts or interface descriptions.

Embed diagrams here or save relative links. Prefer repository formats or editable Mermaid when unspecified. Simple clear designs may use text/tables; do not add components to fill the template. Before complete architecture approval, check that required diagrams are actually filled, understandable, and consistent with this document. Distinguish existing/planned/undecided states, not placeholders. Synchronize diagrams/text as design changes; missing required diagrams leave affected scope incomplete without adding diagram approval. Record rendering checks and unverified work under the workflow.

## Interface and Data Contracts

List important module/service interfaces: inputs/outputs, validation, permissions, error semantics, side effects, and compatibility.

| Data/state | Owning module | Readers/writers and entrypoints | Lifetime/storage | Consistency/compatibility |
| --- | --- | --- | --- | --- |

Explain collaboration interfaces and inaccessible internal data clearly enough to guide implementation.

### Database Implementation Document (Added During Coding)

Architecture addresses storage selection, ownership, and key contracts without requiring an advance database attachment or its approval. Under the [engineering workflow](../../references/en/engineering-workflow.md), output/save database design at database-related coding start, defaulting to `docs/database-design.md`. See the [database design template](database-design-template.md).

- When the document exists or is created during coding, optionally link its path, content version, and scope without duplicating design. Do not label planned links as existing files.
- Inspect existing databases and reuse/update scoped design. Database details are coding deliverables without separate approval. Changes affecting approved requirements, stack, public contracts, module boundaries, or permission/data rules update and reconfirm affected content.

### Server and Older-Agent Matrix (Only When Applicable)

Link requirements' user/project compatibility scope and protocol baseline. Agent is the product client/collector. Analyze changed interfaces, field meanings, errors, and flows, and preservation without upgrading Agents. Do not assume old versions ignore new fields or support new negotiation.

| Server version/planned change | Older Agents and scope basis | Protocol/core flows | Changes/preservation design | Cases/environment | Verification status/evidence |
| --- | --- | --- | --- | --- | --- |

Record plans/unverified items during design, then actual versions/artifacts/results/evidence after implementation. Do not silently omit required versions/scenarios; ask about unverifiable scope. Breaking compatibility, failed/unrun necessary verification, or missing evidence blocks merge/release, not solved through forced upgrades. Mark no client communication not applicable.

## Failure, Security, and Resource Handling

Cover relevant timeouts, cancellation, retries/idempotency, concurrency/cleanup, external input, authentication/authorization, sensitive data, and observability. High-risk changes describe deployment compatibility, migration checks, and feasible recovery.

## Trade-Offs and Open Issues

Record important decisions, alternatives, and costs. Resolve consequential boundary, public-contract, and data-safety issues before affected implementation.

## Requirement-to-Module and Acceptance Mapping

Each current requirement has owning modules and verification; one requirement can span modules.

| Requirement ID | Module/interface | Acceptance | Planned/actual code | Tests/check commands | Implementation state | Verification state/evidence |
| --- | --- | --- | --- | --- | --- | --- |

During design, record plans; nonexistent code/tests are not implemented/not run. After implementation, record actual locations/results. Separate implementation from verification; distinguish passed, failed, not run, and not applicable with reasons. Link existing acceptance records rather than duplicate ledgers.

Check actual calls/imports/data entrypoints against allowed dependencies. Record tooling/local-review coverage; a design table is not implementation proof.

## Implementation Order and Document Changes

After design approval, split work by modules/requirements with prerequisites and inspectable outcomes. Material requirements/boundary changes need an impact record, updated documents, and renewed approval before affected implementation continues.
