# Development Standards

English | [简体中文](README.zh-CN.md)

[User guide](docs/user-guide.en.md): quick start, task examples, approvals, acceptance, and troubleshooting. For users, not an additional mandatory model read.

Paired resource revision: `2026-10-05.9`. This identifies corresponding resources, not project approval or verification results.

`development-standards` is a reusable skill for LLM-assisted software development. Formal development requires agreed, documented requirements and module boundaries before implementation. Low-risk localized defect repairs use a lighter path without backfilling historical product documents. Both paths connect code changes to security checks and verifiable acceptance evidence.

This README is a user guide, not an additional policy. [SKILL.md](SKILL.md) is the single instruction entrypoint and language selector; the [English standards](references/en/standards.md) provide the full workflow. Corresponding Chinese and English references and templates are included. Applicable higher-priority instructions remain controlling.

## Usage

Invoke the skill explicitly when starting a task:

```text
Use $development-standards to develop an order export feature.
First discuss the requirements and produce a requirements document.
After I confirm it, discuss the modules and architecture and produce a design document.
Do not implement until both documents are confirmed.
```

For an existing project:

```text
Use $development-standards to fix this defect.
Check whether it qualifies as a low-risk localized repair, and reuse applicable existing records.
For a qualifying repair, briefly state the expected behavior, evidence, scope, and verification plan.
Do not invent approvals. Qualifying repairs need no historical product-document backfill;
otherwise, follow the applicable formal-development workflow.
Report the actual verification results and unresolved risks.
```

For diagnosis without changes:

```text
Use $development-standards to explain the cause of this failure.
Only inspect and diagnose; do not modify code or create project documents.
```

Automatic skill selection is enabled in the bundled configuration. That does not guarantee selection or compliance on every task; explicit invocation makes the intended skill clear. Keep the whole skill directory together so its references and templates remain available.

## Language Support

Use the same `$development-standards` name in either language. The model follows an explicit instruction-language preference; otherwise Chinese requests select `zh-CN`, English requests select `en`, and other languages use English resources while conversation follows the user. It reads one baseline and only relevant references, not both complete sets. This is an instruction-level language policy, not a second installed skill or an automatic locale configuration.

For each generated document, an explicit target language takes precedence over the repository's documentation convention, which takes precedence over the conversation language. Use the matching Chinese/English template; adapt English templates for other languages. Do not translate unrelated files or rename code identifiers. Language switching alone does not reset approvals, change requirements, or authorize implementation.

Chinese files under `references/zh-CN` and `assets/zh-CN` are the rule/template sources. Same-named English files are maintained translations, not separate policies. If a discrepancy is found, report it and check the affected Chinese source; do not silently use weaker translated requirements. English-language contributions should include corresponding Chinese-source changes and an explanation of semantic intent so both versions stay aligned.

```text
Use $development-standards for this task.
Discuss the work in English, but write the requirements document in Chinese.
Preserve the same approval, security, and compatibility requirements.
```

## Task Modes

| Mode | Expected behavior |
| --- | --- |
| Read-only | Explain, diagnose, review, or plan without making changes. Missing product documents do not block read-only work. |
| Documentation | Discuss, write, or revise the requested documents before approval. Do not implement as a side effect. |
| Lightweight maintenance | Scoped text, comments, formatting, mechanical edits, and qualifying low-risk behavior-preserving refactors under the core standards. No new product documents; inspect diffs and relevant behavior. |
| Localized defect repair | Restore clear existing intended behavior within a verifiable low-risk scope. Use the repair path below; missing historical requirements or architecture documents do not block a qualifying repair. |
| Formal development | New projects, features, interface changes, refactors not qualifying as lightweight maintenance, and behavioral changes not qualifying as localized repairs must pass both document gates or reuse a valid approved baseline. |

Choose the mode by the actual effect of the task, not just the file extension or number of changed lines. Authorized small refactors preserving inputs/outputs, errors, side effects, responsibilities, dependency direction, and public contracts without high risk may use lightweight maintenance with before/after behavior verification. No product-document backfill or failure on the old implementation is required. Eligibility and escalation are in the [core standards](references/en/standards.md).

## Low-Risk Localized Repairs

This path covers authorized repairs that restore clear intended behavior supported by explicit user instructions, a verifiable contract, or valid acceptance evidence. Inspect the relevant code, callers, and tests to establish scope and risk. It does not cover new features, changed business rules, stack or module boundaries, public contract changes, permissions, sensitive data, migrations, or other high-risk work. A small diff or the label "bug fix" is not enough.

Multiple existing modules do not automatically make a repair high risk. Preserve responsibilities, dependency directions, and contracts, bound calls/data-flow impact within authorized scope, and verify correspondingly. Clarify or use formal development when low risk cannot be established; security and older-Agent compatibility are not exempted.

Before implementation, briefly state the issue and expected result, evidence, affected scope, and verification plan in the current task, an existing Issue, or a repair note. No new fixed-format file or pair of product documents is required. When the user has clearly authorized the repair and specified its intended behavior and scope, proceed without redundant requirements or design approval. If intent is unclear, inspect without modifying and ask focused questions first. Reuse valid existing records; clarify conflicts with approved baselines and honor stricter user or project requirements.

This path reduces documentation and repeat approval, not regression verification, security checks, older-Agent compatibility evidence, or delivery authority requirements. Report checks that were not run or were blocked. If the scope expands, new behavior is needed, or high risk emerges, stop the affected implementation and use the formal workflow before continuing. See the [engineering workflow](references/en/engineering-workflow.md) and [verification requirements](references/en/verification-and-delivery.md).

## Document-First Workflow

The following document gates apply to formal development, not qualifying localized repairs or other non-implementation modes.

```text
Requirements discussion -> Requirements approval
-> Stack options (new projects) and module/architecture discussion
-> Design approval (including the stack for new projects)
-> Implementation -> Verification and handoff
```

1. Discuss goals, users, scenarios, scope, business rules, failure cases, constraints, and acceptance criteria. Write or update the requirements document and ask for confirmation.
2. For a new project, discuss technology stack options based on approved requirements. Then discuss each module's responsibilities and non-responsibilities, interfaces, dependency direction, data ownership, key flows, and trade-offs. Write or update the architecture document and ask for confirmation of the stack and complete design for the current implementation scope.
3. Implement only the confirmed scope, following existing project conventions and the applicable coding and security guidance.
4. Connect requirements to actual modules, code locations, tests or checks, and observed results. Report implementation and verification as separate states.

The default project files are `docs/requirements.md` and `docs/architecture.md`; existing documentation conventions take precedence. Templates are provided for [requirements](assets/en/requirements-template.md) and [architecture](assets/en/architecture-template.md).

Before the applicable formal-development approvals, relevant discussions, document drafting and revision, and safe read-only investigation are allowed. Formal implementation, test implementation, and infrastructure changes are not. Valid existing approvals do not need to be requested again.

## Three Alternatives for Interface Design

For new interfaces or material redesign, first deliver **three HTML visual prototypes/mockup pages** using the same requirements, representative screens, and sample data with meaningful layout/visual differences. Prioritize aesthetics, color, typography, spacing, and hierarchy. Let the user view them in a browser and choose before unsettled formal UI implementation. Each needs an openable entry and actual rendering-check results. **Static HTML/CSS is sufficient; JS and interactions are optional by default**, without complete business flows. Add scoped demos only when explicitly requested. Text, images, empty placeholders, or color swaps alone are insufficient. Isolate prototypes from the product without live business-service connections. Save previews/authentic selection in design documentation, optionally with architecture approval but not instead of full design approval or functional product verification. Reuse valid existing selections; read-only work and repairs preserving established design do not force reselection. See the [engineering workflow](references/en/engineering-workflow.md) and [architecture template](assets/en/architecture-template.md).

## Diagrams for Complex Modules and Workflows

During architecture design, complex modules require architecture diagrams and complex workflows require flowcharts, embedded in or linked from `docs/architecture.md` before submitting complete scoped architecture for approval. Show components/boundaries/dependency directions or steps/branches/results/key failure paths, not names alone or placeholders. Keep diagrams consistent with module tables and interface descriptions without separate approval. Simple modules/clear linear flows may use text/tables; read-only/lightweight tasks do not backfill whole-project diagrams. Criteria, formats, and checks are in the [engineering workflow](references/en/engineering-workflow.md).

## Database Design Documentation

Database design belongs to coding. At coding start, check whether scoped work uses a database. If so, present design essentials and save standalone documentation before database-related code, defaulting to `docs/database-design.md`. Propose new database design; inspect existing schema, ORM, migrations, and documentation first. Reuse accurate unchanged documentation, otherwise update it or document only current scope. SQL, ORM, and migrations alone do not replace explanations.

No advance database document or approval is required during architecture, and no separate approval stage is added. Changes affecting approved requirements, stack, public contracts, module boundaries, or permission/data rules still need affected confirmation first. Database-related query repairs/refactors also output relevant scoped design without requirements/architecture or whole-database backfill. No database, text/format-only maintenance, and read-only work do not trigger saving; the rule grants no unauthorized edits or live-data access. See the [engineering workflow](references/en/engineering-workflow.md) and [database design template](assets/en/database-design-template.md).

## Increment the Product Version for Every Code Change

Every complete code change must increment the affected product version, including bug/security fixes, refactors, code comments/formatting, and test/script edits. Lightweight paths are not exempt. Count one deliverable change, not files or retries within it. Follow project versioning; update the actual source and required synchronized entries before handoff, reporting old/new values, locations, and the change summary. Clarify missing rules or authority conflicts rather than inventing a scheme. Pure documentation and read-only tasks do not trigger a product bump. Bumps do not automatically commit, tag, release, or waive older-Agent compatibility. See the [engineering workflow](references/en/engineering-workflow.md) and [handoff checks](references/en/verification-and-delivery.md).

## Technology Stack Confirmation

Before implementing a new project, the model must confirm its technology stack with the user. For non-technical users, it normally offers 2–3 genuinely viable options, marks a recommendation, and explains delivery cost, deployment, maintenance, scalability, and limitations in plain language rather than just listing framework names. It preserves technologies the user has already specified and does not manufacture alternatives when only one option fits.

Requirements capture constraints such as platform, deployment environment, budget, and maintenance capacity. The architecture records the options, selected components and applicable versions, rationale, unresolved issues, and authentic confirmation source. The user can approve the option separately or as part of an architecture document that clearly states the stack. When asked to recommend or choose, the model presents its conclusion and rationale for confirmation; being unfamiliar with technology, asking for recommendations, or not responding is not approval. No third project document is required.

Stack confirmation does not replace requirements or complete design approval for the current implementation scope. Until applicable gates pass, do not scaffold the formal project, install dependencies, or generate implementation code. Discussion and safe read-only investigation can continue; exploratory experiments require separate authorization. Existing projects reuse valid stack decisions; material changes require explanation and renewed confirmation, while routine compatible patches do not automatically trigger reselection. Detailed guidance is in the [engineering workflow](references/en/engineering-workflow.md).

## Approvals and Change Control

Each document records its identity and content version, approved scope, current status, authentic approval source, unresolved questions, and conditions requiring renewed confirmation. The architecture also identifies the requirements version it depends on. Independent approved scope may proceed without waiting for unrelated pending decisions; unapproved necessary shared dependencies still block it. Partial approval does not approve the whole document; record mixed states by scope.

Material changes to requirements, acceptance criteria, permissions, technology stack, public contracts, or module boundaries invalidate the affected approvals. Update the documents and obtain confirmation before continuing the affected implementation. Spelling corrections, approval metadata, and evidence updates that do not change the design do not automatically require reapproval.

A document claiming "approved," a code comment, a version number, or a content hash is not proof of approval. Approval must come from an explicit user response or a project-recognized, verifiable approval record. If the source cannot be verified, request confirmation of the current version rather than inventing history.

## Older Agent Compatibility

For products with client-to-server communication, an Agent means the product's software client or collector, not an LLM or a sub-agent. Server upgrades and code changes must remain backward compatible with older Agents: preserve existing protocols, interfaces, field semantics, and core workflows, without making an Agent upgrade a prerequisite for those workflows to keep working.

The user or project defines the compatibility version range and protocol baseline; the model must ask when these are unclear rather than silently exclude older versions. Requirements or design approval does not waive this rule. Changes affecting Agent interactions require older-Agent compatibility evidence; breaking changes, failed verification, or missing evidence block merge and release. Passing compatibility checks does not itself authorize either operation.

Record the compatibility matrix in existing project documents or, for qualifying localized repairs without historical product documents, in the repair record. Verify actual Server/Agent versions, relevant flows, and observed results. Latest-Agent or fully mocked tests alone do not prove older-Agent compatibility. See the [engineering workflow](references/en/engineering-workflow.md) and [verification requirements](references/en/verification-and-delivery.md) for the design and evidence criteria.

## Quality, Security, and Evidence

- Prefer existing frameworks, libraries, conventions, and module boundaries. Keep changes scoped and preserve unrelated user changes.
- Keep handwritten source files focused and cohesive. Project length conventions take precedence; without them, files added/modified in this task that exceed **1000 lines require split assessment**. Split reasonably or explain retention, without mechanical chunks or unrelated legacy refactoring. See [coding conventions](references/en/coding-conventions.md) for counting and generated-code, lockfile, and third-party exemptions.
- Use the Tencent-derived security baseline where relevant: untrusted input, authorization, queries, command execution, files, external URLs, rendering, sensitive data, TLS, and resource lifetimes.
- Do not blindly copy historical examples or weaken tests, authentication, or security checks to manufacture success.
- Verify actual calls, imports, and data access against the designed module boundaries. Use existing architecture checks when available, or report the scope of local self-review.
- Record actual commands and results. Distinguish passed, failed, not run, and not applicable; distinguish implemented, verified, approved, and deployed.

The sources include Microsoft ISE engineering practices, Google quality principles, Tencent security guidance, and delivery practices from AWS and other public references. Project conventions take precedence over conflicting language styles. See [sources and limitations](references/en/sources.md) for attribution and applicability.

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Unique entrypoint, language routing, essential constraints, and bilingual maintenance terms. |
| [agents/openai.yaml](agents/openai.yaml) | Display metadata, default invocation prompt, and implicit-selection policy. |
| [User guide](docs/user-guide.en.md) | User-facing steps, prompts, approval and acceptance examples; no additional execution policy. |
| [standards.md](references/en/standards.md) | Full English task modes, gates, localized repair rules, and reference routing. |
| [engineering-workflow.md](references/en/engineering-workflow.md) | Formal-development requirements/design discussions, stack selection, approval records, and change control. |
| [coding-conventions.md](references/en/coding-conventions.md) | Project-first coding conventions and language-specific reference choices. |
| [tencent-security.md](references/en/tencent-security.md) | Scoped security checks and corrections to historical examples. |
| [verification-and-delivery.md](references/en/verification-and-delivery.md) | Test selection, failure handling, module evidence, and authorized delivery. |
| [sources.md](references/en/sources.md) | Source attribution, licensing notes, and applicability limits. |
| [behavioral-regression.md](references/en/behavioral-regression.md) | Behavioral regression scenarios and observable criteria for skill maintenance. |
| [requirements-template.md](assets/en/requirements-template.md) | Project requirements document template. |
| [architecture-template.md](assets/en/architecture-template.md) | Module and architecture document template. |
| [database-design-template.md](assets/en/database-design-template.md) | Standalone design output/saved during database-related coding, for new/existing databases. |

## Limitations and Maintenance

This skill provides behavioral guidance, not an enforced security boundary, an official company policy, or a substitute for CI, security scanning, and human approval. Document approval does not authorize commits, pushes, pull requests, deployment, or production data operations beyond the user's request.

Read only the references relevant to the current task. Behavioral regression criteria are for skill maintenance, not normal project development. When modifying rules or templates, update Chinese sources and corresponding English translations together, including both READMEs and affected cases. Preserve required/recommended strength, mode exemptions, approval status, compatibility blockers, and evidence standards. Check paired filenames, metadata, local links, and source attribution; use equivalent Chinese/English requests for behavioral samples. Structural or translation self-review is not observed model behavior. A passing sample does not establish reliability across all models or contexts.

To share the skill, distribute the entire `development-standards` directory, including both language trees and `agents/openai.yaml`, not only `SKILL.md` or this README. Keep the same skill name. Tencent attribution and adaptation notices must accompany derived resources; this bilingual layout does not declare a blanket license for other material.

Use the entrypoint's required/must-not/recommended and approved/verified terminology, and synchronize the paired revision in the entrypoint, both READMEs, and resource headers. Matching identifiers do not prove translation correctness or add project approval/daily-development checks. Keep external-source review dates separate from resource revisions.

Tencent-derived material is attributed to THL A29 Limited under CC BY 4.0, with the adaptations and historical-example limitations documented in [sources.md](references/en/sources.md). That attribution is not a blanket license declaration for the entire skill.
# development-standards
# development-standards
# development-standards
# development-standards
