# Development Standards

English translation | [Chinese rule source](../zh-CN/standards.md) | Paired revision: `2026-10-05.9`. Language selection and terminology are defined in the [skill entrypoint](../../SKILL.md).

Goal: deliver changes that meet requirements, are maintainable, and have verification evidence, not merely generated code that runs. This skill is a cross-project development baseline, not an official universal company policy or a substitute for human approval, tests, or CI gates.

## Scope and Rule Levels

- **Required**: Applies in the relevant scenario. If unmet, correct it, report the gap, or request the necessary decision; do not mark the work complete.
- **Recommended**: Prefer it; adapt to project conventions, compatibility, or cost and explain important trade-offs.
- **Project conventions**: Explicit repository rules govern naming, formatting, frameworks, directories, test commands, coverage, and approval counts.
- Follow higher-priority instructions, user authorization, and repository rules. Do not silently override local standards; explain conflicts and use an approach meeting the safety objective.
- When the user asks only for explanation, diagnosis, review, or planning, do only that. Discovering an issue does not authorize repair, deployment, or external operations.

## Task Modes and Formal-Development Gates

Select a mode by the actual task. Start, stop, and completion conditions use that same mode, not merely the file extension.

| Mode | Application of document gates |
| --- | --- |
| Read-only: explanation, diagnosis, review, planning | Do not modify files or refuse read-only work because product documents are missing. |
| Documentation: discuss, write, or revise requirements, architecture, or standards | Edit documents within the task before approval. Material changes to approved business/design content invalidate affected approvals; do not implement as a side effect. |
| Lightweight maintenance: text, comments, formatting, mechanical edits, or qualifying low-risk behavior-preserving refactors below | Do not require new or approved requirements/architecture documents. Database-related coding still follows the design-output rule below; text/format-only work does not trigger it. Check scope, diff, and applicable checks. |
| Localized repair: restore clear intended behavior in a verifiable low-risk existing defect | Use the repair path below. Missing historical requirements/architecture documents do not block qualifying repairs or require those two files. |
| Formal development: new projects, features, interface changes, refactors not qualifying as lightweight maintenance, or behavioral changes not qualifying as localized repairs | Pass the following gates or reuse an authentic approved baseline applicable to the current scope. |

Formal development creates and approves separate requirements and architecture documents in order. Before requirements approval, discuss/edit requirements and investigate read-only; do not start formal architecture or implementation. After requirements approval, discuss module responsibilities, interfaces, dependencies, and data ownership; new projects also require explicit stack approval. Implement only after complete design approval for the current implementation scope. Partial approval covers only identified scope, not the whole document; necessary dependencies must also be approved. Independent approved scope may proceed without unrelated open issues blocking it. Before applicable gates pass, do not scaffold the formal project, install dependencies, write formal code/tests, or change infrastructure. Experiments need separate scope authorization. Record the stack in architecture, not a third document; asking the model to recommend, a model default, or silence is not stack approval.

Default documents are `docs/requirements.md` and `docs/architecture.md`; repository conventions take precedence. Without a baseline, document only the current scope. Approval identifies content version, scope, and an authentic verifiable source, not a file's "approved" label or model self-review. Reuse valid approvals; request current-version confirmation when unverifiable. Before material requirements, stack, public-contract, or module-boundary changes, update affected documents, invalidate affected approvals, and obtain renewed confirmation. Detailed discussion, stack recommendations, approval fields, and invalidation rules belong in the [engineering workflow](engineering-workflow.md).

During architecture design, complex modules require architecture diagrams and complex workflows require flowcharts, saved with architecture and consistent with responsibilities, interfaces, and failure handling. Missing required diagrams means the scoped complete design is not ready. Diagrams do not replace written contracts or add separate approval. Complexity criteria, diagram contents, and maintenance are in the [engineering workflow](engineering-workflow.md). Simple designs may use text/tables; read-only/lightweight tasks do not backfill whole-project diagrams.

## Three Visual Alternatives for Interface Design

When scoped work creates, redesigns, or materially changes interface layout, information hierarchy, visual style, or key interactions, provide **three selectable visual alternatives** and obtain the user's choice before implementing the unsettled UI. Formal development does this during architecture/interface design after requirements approval, not by implementing pages first and seeking retroactive approval. Standalone design tasks produce artifacts only within authorized design scope, without automatically authorizing product coding.

Use the same requirements, representative screens, sample data, and target viewports across all three, with meaningful differences in layout/navigation, density, typography, and visual hierarchy. Color swaps or three textual style names are insufficient. Each must deliver a browser-openable **HTML visual prototype/mockup page** emphasizing aesthetics, color, typography, spacing, component styling, and content organization appropriate to users, product context, and the existing design system. Unstyled wireframes or empty placeholders are insufficient. **Static HTML/CSS is sufficient; JavaScript and lightweight interactions are optional by default, without required complete navigation, form validation, state management, or business flows.** Low-cost lightweight interactions may be added as needed. Honor explicitly requested interaction demos within their specified scope, not three complete products. Images may supplement, but standalone images/text cannot replace HTML entries. Provide each entry, differences, suitability, and consequential trade-offs; actually check rendering and disclose unverified work without claiming functional implementation. Save in existing design documentation or link resources from `docs/architecture.md`, recording the selected option/version and authentic user source. Recommendations, silence, or stack approval are not a UI selection; UI selection is not full architecture approval.

Within authorized interface-design scope, create and locally preview isolated HTML/CSS visual pages, adding JS only when needed, as design artifacts rather than formal product implementation. Use sample data without product scaffolding, formal project dependencies, or live business services/sensitive data. New tools, external publication, and real operations retain applicable authority requirements. A script/interaction-execution prohibition alone permits JS-free static pages; prohibited or unavailable browser previews require disclosure of unverified work, not unauthorized actions or invented displayed results.

Reuse an explicit applicable existing selection. Implementing it, read-only reviews, and localized repairs/text corrections preserving established design do not force three new options. Actual redesign applies this rule to current scope; provide three when the current user explicitly requests them. For a requested combination, show the revised result and confirm it without reselecting unrelated screens. See the [engineering workflow](engineering-workflow.md) and [verification and delivery](verification-and-delivery.md).

## Low-Risk Behavior-Preserving Refactors

- Use only for authorized existing-code cleanup with verifiable impact, such as extracting a private function or eliminating duplication within one module. Inspect actual callers, data flows, and tests. Preserve inputs/outputs, error semantics, side effects and call order, business rules, stack, module responsibilities/dependency directions, and public contracts. Exclude permissions, sensitive data, migrations, concurrency/resource lifetimes, production changes, and other high risk. A "refactor" label, small diff, or green tests alone do not establish eligibility.
- Briefly record the goal, scope, preserved behavior, and verification in the current task, an existing Issue, or maintenance note. Proceed when authorized and eligible without historical product-document backfill or repeat design approval. Reuse effective tests; add behavior protection as needed and compare results before/after, including errors and side effects. Compilation alone is insufficient; do not apply a defect repair's "old implementation fails" requirement to a behavior-preserving refactor.
- Clarify ambiguous intent or unbounded impact. If business/contracts/boundaries must change or high risk appears, stop affected refactoring and use the formal workflow. Honor stricter project rules, security, older-Agent evidence, and delivery authority. Report unverified work honestly.

## Low-Risk Localized Repair Path

- Use only for authorized repairs of existing defects. Intended behavior needs explicit user instructions, a verifiable contract, or valid acceptance evidence; inspect code, callers, and tests to establish low-risk impact. Do not add features or change business rules, stack, module boundaries, or public contracts, or involve permissions, sensitive data, migrations, or other high risk. Line count, a single file, or the current incorrect implementation is not sufficient justification.
- Involving multiple existing modules does not automatically disqualify a repair. It must remain within authorized scope, preserve responsibilities, dependency directions, and contracts, have bounded call/data-flow impact, and have corresponding regression verification. Multiple files are not necessarily multiple modules. If low risk cannot be established, clarify or use the formal workflow; this is not a high-risk exemption.
- Before implementation, briefly state the issue and expected behavior, evidence, affected scope, and verification plan in the current task, an existing Issue, or a repair note. No new fixed-format file is required. If the user clearly specified intent, scope, and repair authorization, proceed without redundant requirements/design approvals. If ambiguous, inspect read-only and ask focused questions; do not fill gaps with guesses or fabricated file approvals.
- Reuse applicable documents, tests, and authentic approvals. Missing historical product documents need no backfill. Clarify conflicts with approved baselines; business/contract changes use the formal process. Honor stricter project or user requirements rather than bypassing them through this path.
- Provide regression verification, relevant checks, and self-review evidence; reuse effective existing cases. Report checks not run or blocked by the environment honestly. If scope expands, new behavior is needed, or high risk emerges, stop affected implementation, update affected requirements/design through the formal workflow, and obtain confirmation. Security, older-Agent compatibility, and commit/release authority are not waived.

## Assess Impact First

Read applicable `AGENTS.md`, relevant requirements/design records, actual code and tests, and build/format configuration. Load task-relevant content, not the entire repository just to collect context.

Classify by consequences, not line, file, or module count. Changes to module responsibilities/dependency boundaries or public contracts, and work involving authentication/authorization, sensitive data, migrations, concurrency/resource lifetimes, or production changes are high risk. Address failure, compatibility, and recovery in applicable document gates and verify specifically; pause affected work for missing consequential decisions. One-line authorization changes can still be high risk, and new facts can upgrade risk. Ask focused questions for missing consequential correctness, authorization, data-safety, or contract information. Label minor assumptions; do not use them to bypass approval.

## Load References as Needed

- For formal-development gate checks or project-document discussion/creation/updates, read the [engineering workflow](engineering-workflow.md), including approval records, requirements/architecture templates, and the conditional database design template. Lightweight or read-only tasks need not load the full workflow.
- To choose language-specific rules, introduce coding patterns, or change interfaces, read [coding conventions](coding-conventions.md). Do not replace explicit existing configuration with a different style.
- Whenever modifying executable code, changing security behavior in configuration, or handling external input, permissions, files, networks, or secrets, read the [Tencent-derived security baseline](tencent-security.md). Apply only relevant checks; do not expand into a repository-wide security audit.
- For localized repairs, behavior-preserving refactors, routine/high-risk implementation, test changes, or release work, read [verification and delivery](verification-and-delivery.md).
- For attribution, historical examples, or skill updates, read [sources and limitations](sources.md). Normal development need not repeatedly download manuals.
- For maintenance or behavioral testing of this skill, read [behavioral regression cases](behavioral-regression.md). Do not load evaluation criteria for normal project development.

## Implementation Constraints

- At coding start, check database involvement and apply the design-output requirement below. Skip it when no database is used; do not introduce a database to fill a template.
- Understand relevant behavior, callers, and tests before editing; preserve existing user changes.
- Focus on one verifiable objective. Separate broad renaming, formatting, and dependency upgrades from functional changes unless needed to complete the task.
- Prefer existing modules, frameworks, and proven libraries. Add abstractions only for actual complexity, not speculative future needs.
- Keep module responsibilities and dependency direction clear; avoid cross-layer access, cycles, duplicated business rules, and hidden shared mutable state.
- Keep handwritten source files focused on a single, clear responsibility. Follow project length conventions first; without them, files added or modified in this task that exceed **1000 lines require split assessment**. Split reasonably or explain retention without mechanical chunks or unrelated refactoring. See [coding conventions](coding-conventions.md) for counting, exemptions, and authority boundaries.
- Use structured parsers, parameter binding, and typed/data contracts rather than string concatenation in place of available safe APIs.
- Names communicate business meaning; comments explain constraints, trade-offs, or non-obvious reasons. Interface documentation describes inputs, outputs, and errors.
- Do not swallow errors or disguise them as success. Handle timeouts, cancellation, retries, cleanup, and concurrency boundaries as applicable.
- Explain new dependencies' purpose, version compatibility, maintenance, and licensing risk. Do not bulk-upgrade or introduce a different stack as a side effect.
- Do not skip tests, remove valid assertions, disable authorization/TLS verification, or weaken security checks to make tests pass. Explain genuine contract changes before synchronizing code and tests.

## Database Design Output During Coding

When scoped coding uses a database, present the design essentials to the user and save a standalone database design document before related queries, SQL, ORM, or migration code. Default to `docs/database-design.md`. For a new database, describe scoped entities/relationships, fields/constraints, access/indexes, and applicable transactions/ownership. For an existing database, inspect relevant schema, ORM, migrations, and design records first; verify the current design, reuse/update documentation, and distinguish existing behavior from proposed changes. If accurate documentation already covers unchanged scope, provide its path/version and essentials without duplicating it. If absent, document only the affected scope, not the entire database history. Mark unverifiable details unknown; do not access live databases without authority.

This conditional coding deliverable need not be produced or approved during architecture and adds no separate approval round. Architecture still addresses storage selection, module ownership, and key data contracts. Implementation details within approved scope do not automatically invalidate architecture approval. Database-related localized query repairs/refactors also output/save their scoped design, without backfilling requirements/architecture or repeat approval. Material changes to approved requirements, stack, public contracts, module boundaries, or permission/data rules require affected documentation and renewed confirmation first. Migrations, destructive operations, and live-data access require separately scoped authority and safety decisions.

No database, text/format-only maintenance, and read-only diagnosis/review/planning do not trigger saving. Read-only work grants no documentation-edit authority. SQL, ORM, and migrations alone cannot replace explanations; keep documentation and implementation consistent as they evolve. Details and templates are in the [engineering workflow](engineering-workflow.md).

## Product Version Increments During Coding

Every project-code change (addition, modification, or deletion) must increment the affected product version, including features, bug/security fixes, refactors, and changes to code-file comments, formatting, tests, or scripts. Lightweight maintenance and localized repairs reduce documentation/repeat approval, not versioning. Small changes or the absence of a release are not exemptions.

Increment once per complete, deliverable code change, not per file, edit action, or test retry. Resuming the same undelivered change with a correct existing bump does not increment again; modifying an already delivered version requires another increment. First inspect the actual product version source and project increment scheme. Before handoff, update that source and required synchronized entries, reporting old/new versions, locations, and a change summary. Clarify missing/conflicting rules or explicit prohibitions on version-file edits; do not invent a scheme or edit without authority. See the [engineering workflow](engineering-workflow.md).

Pure documentation and read-only diagnosis/review/planning do not trigger a product bump. Document content versions, skill paired revisions, dependency/protocol versions, and database migration identifiers cannot substitute for the product version. A bump does not automatically invalidate requirements/architecture approval, prove tests passed, authorize commits/tags/merge/release, or waive older-Agent compatibility.

## Older-Agent Compatibility Redline

Applies to products with client Agents communicating with a Server. Agent means the product's software client or collector, not an LLM or subagent.

Server upgrades or code changes **must remain backward compatible with older Agents**. Preserve existing communication protocols, interfaces, field semantics, and core workflows; do not make forced Agent upgrades a prerequisite for normal operation after a Server upgrade. Changes breaking this compatibility must not be merged or released. Changes affecting Agent interactions must provide older-Agent compatibility verification evidence.

The user/project defines supported version scope, protocol baseline, and core workflows. Ask if unclear; do not set a minimum version, narrow scope, or declare older versions unsupported unilaterally. Requirements/design approval does not waive this redline.

If an Agent-interaction change is incompatible, verification fails, or evidence is missing, do not mark it mergeable/releasable or perform merge/release. You may hand off a pending-review patch with explicit blockers. Forced upgrades, latest-Agent-only testing, and fully mocked tests cannot replace compatibility proof. See the [engineering workflow](engineering-workflow.md) for design and [verification and delivery](verification-and-delivery.md) for evidence criteria.

## Verification and Self-Review

- After final edits, run checks proportionate to risk and record actual commands, exit status, and results. Defect repairs need regression verification detecting the original issue. Execution is not success; distinguish not run, environmental blockers, pre-existing failures, and new regressions.
- Self-review the full diff, relevant calls, and dependencies against this mode's goals, scope, contracts, and security requirements. Do not call self-review independent review or waive required human approval.
- Each formal-development requirement needs module ownership and acceptance, linked to actual code, check locations, and results. Record planning, implementation, and verification separately; directory lists and design tables are not architecture/implementation evidence. Detailed scenario selection, failure handling, and delivery evidence belong in [verification and delivery](verification-and-delivery.md).

## Stop Conditions and Handoff

Only formal development waits at the relevant discussion stage for missing approved documents. Continue in-scope discussion, document editing, and read-only investigation rather than blocking documentation, lightweight maintenance, or qualifying localized repairs. Clarify ambiguous repair/refactor intent; scope/risk increases use the formal workflow. Other stop conditions apply to affected operations: material scope expansion, module/public-contract changes, new external/production authority, missing migration/authorization decisions, unknown data recovery, or unmet critical security requirements. Clearly understood safe portions can continue.

Keep the final report short, but include:

- Current stage, actual changes, and acceptance results. Formal development/product-document work reports document locations and approval status; localized repairs or behavior-preserving refactors report goal, scope, and verification basis without requiring two product documents. Other lightweight/read-only work does not require those files either.
- Actual passed/failed checks; consequential checks not run or not applicable and why.
- For code changes, old/new product versions, actual edited locations, and required synchronized entries. Disclose unmet versioning requirements rather than marking the task complete.
- Unresolved risk, compatibility/migration effects, and necessary approval or next steps.

"Implemented," "verified," "approved," and "deployed" are separate states supported by separate evidence. Do not commit, push, create PRs, deploy, or change external systems unless requested and authorized.
