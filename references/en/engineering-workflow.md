# Engineering Workflow

English translation | [Chinese rule source](../zh-CN/engineering-workflow.md) | Paired revision: `2026-10-05.9`

Use Microsoft ISE Playbook's Ready/Done, design review, and engineering checklists as process references. The requirement to approve requirements, confirm a new project's stack, approve module/architecture design, and only then implement is a user-defined gate; qualifying low-risk localized repairs use a lightweight path. Neither policy claims all major companies share this approval system. See [sources.md](sources.md).

## Select the Task Workflow First

Use the task modes in the [core standards](standards.md). The requirements/design gates and approval records below apply to formal development. Missing two approved product documents must not block read-only work, documentation, lightweight maintenance, or qualifying localized repairs. The core defines low-risk behavior-preserving refactor eligibility and before/after verification; a defect repair's old-implementation failure condition does not apply.

### Low-Risk Localized Repairs

Eligibility, the brief repair statement, clarification, and escalation are defined once in the [core standards](standards.md); verification and records are in [verification and delivery](verification-and-delivery.md). Qualifying repairs do not use the two formal-development document gates below. Assess multiple existing modules by actual impact, not module count; high-risk, security, and older-Agent evidence requirements remain applicable.

## Stage One: Discuss and Document Requirements

Read existing records, actual implementation, and relevant constraints. Distinguish approved facts, model assumptions, and unresolved user decisions. Ask focused questions by impact: establish goals/boundaries before business rules and acceptance. Do not give the user a long questionnaire unrelated to the current project.

Cover at least:

- Target users, problem, typical flows, and intended outcomes.
- Included/excluded scope and existing behavior that must remain unchanged.
- Functional rules, inputs/outputs, boundaries, failures, and applicable permissions, privacy, and data ownership.
- Dependencies, compatibility, and applicable performance/capacity/availability goals; do not invent metrics.
- For new projects, collect platform, deployment conditions, budget, maintenance capacity, existing systems, and specified technologies. Ask non-technical users about goals/constraints, not for a framework choice upfront.
- For client Agent/Server communication, establish older-version compatibility scope, its source, and required protocols/core workflows. Ask if unclear; do not retire older versions unilaterally.
- Observable acceptance criteria for each requirement and whether unresolved issues affect design/implementation.

Use the repository's format; otherwise choose the [English requirements template](../../assets/en/requirements-template.md) or [Chinese requirements template](../../assets/zh-CN/requirements-template.md) according to the document's target language, and save to `docs/requirements.md`. Large projects may split by feature with a clear entrypoint. Stable requirement IDs such as `REQ-001` help module/acceptance mapping; no universal numbering scheme is required.

The document must contain actionable rules, acceptance, non-goals, unresolved issues, and discussion conclusions, not just a transcript or feature names. Mark missing information as pending confirmation rather than presenting model inference as business fact.

After writing, give the user the path, key conclusions, and consequential open issues, and request approval. Only after explicit confirmation of the current content and scope should you record its source/scope and begin architecture discussion. Creating a file does not pass the gate; the original development request does not approve a later draft.

## Stage Two: Discuss and Document Modules and Architecture

### Confirm the New-Project Stack First

Choose candidates based on approved requirements, not unresolved business features. Preserve user-specified technologies and constraints; explain conflicts and ask for a decision rather than silently replacing them. Existing projects reuse applicable approved stacks; an ordinary defect repair is not stack reselection.

For non-technical users, normally offer 2-3 viable combinations and mark a recommendation. Explain when only one option fits, and do not ask users to reselect explicitly chosen technologies. Compare combinations rather than tool names; describe language/runtime, client/frontend, server, storage, tests/build, and deployment as relevant. Mark unnecessary components as unnecessary; do not add databases, microservices, or cloud services to fill a table.

| Option and rationale | Plain-language explanation and use | Main technologies | Delivery/operating cost and maintenance | Scalability, limitations, and risk |
| --- | --- | --- | --- | --- |

Explain user-visible differences before technical names; do not expect selection based on unfamiliar abbreviations. Distinguish evidence, estimates, and unknowns for cost, time, and performance. Check current official sources for versions, maintenance, licensing, or prices when needed; record consequential unverified details rather than relying on outdated memory.

Ask the user to select or approve the recommendation. Approval can accompany an architecture draft clearly stating the stack; unresolved options remain draft, not final decisions. A request to recommend or choose, or "I don't know technology," is not approval of a specific stack: present the conclusion and rationale for confirmation.

Record the selected stack, key components and compatible versions/ranges, rationale, authentic approval source, and applicable scope in the architecture document. If only part of the stack is specified, preserve it and ask only about remaining consequential correctness, cost, deployment, or maintenance choices; do not require approval of every transitive dependency. Stack approval neither approves the full design nor authorizes paid resources, deployment, or external operations.

Before stack and complete-design gates for the current implementation scope pass, do not scaffold the formal project, install project dependencies, or generate formal code/tests. Read-only investigation and document work can continue. Experiments need explicit authorization and isolation as described below. For material changes to the main language/framework, storage, or deployment model, explain compatibility/cost/maintenance impact, update the design, and obtain renewed approval. Routine compatible patches within the same constraints do not automatically invalidate approval.

### Module and Architecture Design

Divide responsibilities from approved business scenarios after checking existing modules/framework ownership. Reuse boundaries; do not default to microservices or extra layers. Discuss important trade-offs, why modules are organized that way, how they collaborate, and major failure paths.

Use the repository's format; otherwise choose the [English architecture template](../../assets/en/architecture-template.md) or [Chinese architecture template](../../assets/zh-CN/architecture-template.md) according to the document's target language, and save to `docs/architecture.md`. Adjust depth to scale and risk, but cover:

| Topic | Required content |
| --- | --- |
| System boundary | Internal/external participants and dependencies; important call/data flows. |
| Stack | Languages/frameworks, storage, build/tests, deployment, applicable versions; new-project options and approval source/scope. |
| Modules | Responsibilities and non-responsibilities, owning code paths, interfaces, allowed dependency directions. |
| Contracts and data | Inputs/outputs, errors, side effects, ownership/read-write authority, relevant consistency/transaction/compatibility changes. |
| Failures and resources | Relevant timeouts, cancellation, retries/idempotency, concurrency, cleanup. |
| Non-functional and security | Applicable performance, observability, permissions, privacy, recovery goals. |
| Trade-offs and verification | Important alternatives, rationale, unresolved issues, verification of key assumptions. |
| Requirement mapping | Modules implementing each current requirement and acceptance locations. |

Use a module table showing responsibilities, exclusions, paths, interfaces, and dependencies, not merely a directory tree or component names. Describe important flows from entry through business processing, storage/external calls, and error handling. Complex modules/workflows require diagrams under the diagram rules below, not instead of contracts. Mark nonexistent paths as planned, not implemented.

Give business rules clear ownership. Do not delegate authorization to clients, duplicate rules across modules, or bypass interfaces to modify another module's internals. Layer/module/service counts are not quality measures.

### Present Three Visual Alternatives Before Interface Implementation

For new interfaces or material redesign, use approved requirements to present three alternatives for user selection during this stage. Standalone design tasks stay within authorized design scope without forcing product coding. Check target users, core tasks, representative screens, platforms/viewports, and existing brand/design systems. All three preserve the same business, security, accessibility, and project constraints; do not change features, permissions, stack, or add unrelated screens to fill the count.

- Identify three meaningfully distinct designs as A/B/C without mandating three fixed styles. Use the same content, sample data, target sizes, and representative screens/key tasks. Differences can include navigation/layout, density, typography/visual hierarchy, and control/action organization. Color/name swaps or infeasible filler options are insufficient.
- Each must deliver a browser-viewable HTML visual prototype/mockup page, using static HTML/CSS by default; JS is not required. Prioritize aesthetics, layout proportions, color, typography, spacing, component consistency, hierarchy, and content organization suited to the product and existing design system. Text-only options, unstyled wireframes, empty placeholders, or color swaps are insufficient. Build only representative screens/states needed to choose visual direction, not three complete products. Provide entries, suitability, differences, and consequential trade-offs; recommendations do not replace selection. Images may supplement, but cannot be the only deliverable without HTML pages.
- Buttons, navigation, forms, filters, dialogs, and business flows need not be fully operable. Validation, state management, APIs, and login are not required. Low-cost lightweight interactions that help visual comparison are optional; implement and check only the scoped interaction demos explicitly requested by the user, not every feature. Static controls are not visual-prototype defects, but unimplemented functionality cannot be claimed usable.
- Prototypes are isolated design artifacts using synthetic sample data. Explain visual-only scope and relevant unimplemented functionality in design records/handoff without claiming business completion. Authorized interface design permits HTML/CSS creation/local preview, adding JS when needed, not formal scaffolding, project dependency installation, or live services/credentials/sensitive data. New tools, external writes, and real operations retain applicable authority requirements. A script/interaction prohibition alone uses JS-free static pages; a browser-preview prohibition requires no unauthorized preview and an unverified-rendering report.
- Default to `docs/ui/option-a/index.html`, `option-b/index.html`, and `option-c/index.html`, preferring established repository locations. Save relatively referenced assets with prototypes. Prefer lightweight directly openable HTML and actual file links. If a local server is necessary, use available tools and a free port with local-only access, reporting its actual URL and run method without upload/publication. Quickly check entries, assets, and visual rendering/readability/overflow/overlap at representative target viewports. No default per-control interaction or end-to-end testing is required. Report actual rendering checks and unrun work. See [verification and delivery](verification-and-delivery.md).
- Save all three preview references, option versions/scope, comparisons, and authentic selection in existing design records or architecture. Without an existing location, link `docs/ui/` resources from `docs/architecture.md` rather than adding a fixed approval ledger. Selection can be separate or part of architecture approval explicitly including the UI option. Recommendations, silence, the initial development request, and stack-only approval are not selection. UI selection neither approves all architecture nor authorizes unapproved product code.
- For requested combinations/adjustments, show the revised result and confirm affected content before implementation. Reuse valid selections covering current scope; implementing the same design and repairs/text corrections preserving it do not require reselection. Actual redesign presents three new options for affected scope; an explicit current request for three cannot be waived by old selections. Do not invalidate unrelated screens or approvals.

Missing three HTML visual prototypes or user selection leaves affected UI incomplete/pending selection; do not implement that unsettled formal UI. Missing optional interactions cannot disqualify an otherwise suitable static HTML option or block independent approved non-UI scope. Formal work still passes requirements, stack, and complete scoped architecture gates. Products without a UI need no empty options or added interface.

### Required Diagrams for Complex Modules and Workflows

Assess complexity within the current architecture scope. Layered responsibilities or internal submodule collaboration, cross-dependencies, multiple external participants, or workflows with branching, async/concurrent work, retry/compensation, or state transitions require diagrams when structure or execution paths are not clear in a brief linear description. Do not judge solely by module/file counts or code size; a single module can have complex internal flows.

- Complex modules require architecture diagrams showing relevant internal components, module boundaries, key external dependencies, and call/dependency or data-flow directions. Label edges and match module-table nodes; component names arranged without relationships are insufficient.
- Complex workflows require flowcharts showing entry, key steps and owning modules, decision conditions/branches, termination/results, and key failure paths. Show actual concurrent joins, retry conditions/limits, or compensation as applicable without inventing mechanisms. Sequence/state diagrams may supplement multi-party timing or state changes, not replace required flowcharts.
- Simple modules and clear linear flows may use text/tables with optional diagrams. Do not add layers, services, nodes, or whole-project diagrams to fill this rule. Read-only work does not authorize new diagram files; qualifying lightweight repairs/refactors do not backfill historical architecture diagrams. If a change requires formal architecture, apply the rule to its current scope.
- Save diagrams with architecture before submitting it for approval, embedded or relatively linked. Use repository-supported formats; without a convention, prefer editable inline Mermaid. Do not require new drawing-tool installation or a separate approval ledger. Check syntax, links, arrow meaning, and readability. Where a renderer is available, check actual display; disclose unrendered portions rather than claiming rendering was verified.
- Distinguish existing, planned, and undecided content. Match module tables, interface contracts, and failure handling. Synchronize diagrams and text when design changes. Accurate added diagrams or layout-only edits do not automatically invalidate approval; material design changes still use affected reapproval.

Missing required scoped diagrams, placeholder-only graphs, or contradictions leave that scope an incomplete draft. Correct them before submitting it as complete architecture. Diagrams and text share the same architecture approval, not a separate diagram gate; unrelated scope need not wait.

Architecture addresses storage selection, module data ownership, and key data contracts. It need not produce detailed database documentation or include it as an approval attachment. Database design output belongs to Stage Three's coding-start check below. Existing database design may inform architecture without being regenerated.

Submit architecture and trade-offs for approval. Begin implementation only after scoped module/architecture approval and no consequential requirement-mapping gaps. Requirements approval is not design approval. If architecture discussion requires changing business requirements, return to stage one to update and confirm affected requirements.

## Document State and Implementation Gates

The two formal-development documents each identify current state, applicable scope/version, unresolved issues, and authentic approval records. States include draft, pending approval, approved, and reapproval required. Records must come from real user feedback; do not invent reviewers, dates, or opinions.

### Minimum Approval Record

Reuse existing formats, but both document types must locate:

| Field | Requirement |
| --- | --- |
| Identity and version | Path/stable ID and current content version. Approval status and implementation evidence can be separate; neither is a content version. |
| Scope | Current features/requirement IDs and important non-goals. Partial approval does not approve the whole document. |
| Current state | Draft, pending, approved, or reapproval required, according to facts. |
| Authentic source | Explicit current user feedback or a project-recognized verifiable record tied to content version. Do not invent message IDs or reviewers. |
| Open issues | Question, impact, and whether it blocks current scope; identify when none block it. |
| Reapproval triggers | Material requirements/acceptance, permission/data rules, stack, public contracts, module responsibility/dependency changes. |

Architecture also identifies the requirements version and scope it depends on. On resumption, verify current content matches approval records; a file's "approved" label is insufficient. If an old source cannot be verified, explain the gap and request current-version confirmation, not invented history. Once the user explicitly confirms the applicable version now, do not demand the original conversation.

Material requirements/acceptance changes invalidate affected requirements and dependent architecture approvals. Material stack/design/contract/module-boundary changes invalidate affected design approval. Mark affected versions/scope, stop corresponding implementation, update documents, and request confirmation. Spelling, formatting, approval metadata, and design-preserving implementation evidence do not automatically invalidate approval. Assess semantics; do not conceal business changes as document edits.

Versions or optional content fingerprints identify content, not approval. Reuse authentic applicable approvals without making every execution a new approval round.

Database documentation is not a third approval gate here; output/save it in Stage Three. Database implementation details within approved architecture scope do not automatically invalidate approval, and unapproved details must not be labeled approved. Changes affecting approved requirements, stack, public contracts, module boundaries, or permission/data rules still update and reconfirm affected content under this section.

Only formal development checks before implementation that current-scope requirements and complete design are approved, a new project's stack has explicit verifiable approval, necessary dependencies and consequential blockers are resolved, and every current requirement has module ownership and acceptance. Future-iteration issues may remain explicitly out of scope; do not pretend all issues are resolved.

For example, when REQ-001 requirements and complete design are approved and necessary shared dependencies are approved, implement REQ-001 even if independent REQ-002 remains pending. Do not implement REQ-002, mark the whole document approved, or enlarge approval scope. An undecided shared contract required by REQ-001 still blocks it. Record mixed states by scope, reuse authentic approvals, and do not create a duplicate approval ledger.

Reuse approved documents covering current scope when still valid. Repairs meeting original acceptance without changed interfaces/boundaries do not redo architecture. Formal development lacking a baseline documents only affected scope. Exemptions for other modes are defined in the [core standards](standards.md). Issues, chat, or ADRs can carry repair goals, evidence, and results but do not replace the two formal-development document types.

Unapproved formal development stays at the relevant stage while allowing questions, discussion, document writing/revision, authentic approval records, code reading, and safe read-only checks. Formal implementation, test implementation, and infrastructure changes are prohibited. The authorized interface HTML design prototypes above follow this stage's creation/local-preview rules without repeat authorization. Other exploratory prototypes/experiments first need explicit scope authorization, isolation, and recorded results. Prototypes/experiments do not replace design or approval; read-only tasks do not authorize document edits either.

## Stage Three: Output Database Design During Coding

At the start of authorized coding, determine whether scoped implementation uses a database. If the dependency becomes apparent later, perform this check immediately. Formal work retains the requirements, stack, and module/architecture gates above; qualifying repairs/refactors retain the core lightweight paths. Without a database, report not applicable; do not create an empty document or add storage to fill a template.

If a database is used, present the scoped design essentials and save a standalone document before related queries, SQL, ORM, or migration code. Chat alone or post-completion documentation is insufficient. Default to `docs/database-design.md`; prefer existing standalone documents, data dictionaries, or design entrypoints, identifying path, content version, and scope. Choose the [English template](../../assets/en/database-design-template.md) or [Chinese template](../../assets/zh-CN/database-design-template.md) by document language.

- New database: describe a design meeting current requirements and the selected storage approach, distinguishing planned/existing state, key trade-offs, and open decisions.
- Existing database: first inspect relevant schema, ORM, migrations, and design records; verify structure/semantics rather than invent a redesign. If accurate documentation covers unchanged scope, output its path/version and relevant essentials. Update it before changes; if absent, document only scoped entities/access paths, not the entire database history. Identify conflicting evidence or unknown critical structures and ask when needed; do not connect to production databases on your own.
- Database-related query repairs/refactors also output/save scoped design, which may be concise. This does not require requirements/architecture backfill or repeat approval. If the user prohibits documentation edits, explain the saving/authority conflict and obtain necessary permission instead of skipping the requirement or writing without authority.

| Content | Explain within actual scope |
| --- | --- |
| Basis and scope | Related requirements, architecture when available, and modules; sources, inclusions/exclusions, existing/planned state. |
| Entities and relationships | Relevant tables/collections, entities, relationships/cardinality; text or diagrams, not names alone. |
| Fields and constraints | Business meaning, types, nullability, defaults, identifiers/keys, uniqueness, applicable references/validation. |
| Indexes and access | Queries/access paths, indexes and trade-offs; no invented performance metrics or database capabilities. |
| Ownership and consistency | Module read/write entrypoints, permissions, sensitive data/lifecycle, relevant transaction/consistency boundaries. |
| Changes and verification | Current/proposed differences, data/consumer compatibility; applicable migration order, checks, failure handling, feasible recovery. |

Scale detail to size/risk and the actual relational/non-relational model; do not introduce inapplicable tables, foreign keys, or transactions. This is a coding deliverable, not a separate approval stage or a default wait for database-document approval. Implementation detail within approved scope may proceed after recording trade-offs. Material changes to approved requirements, stack, public contracts, module boundaries, or permission/data rules require affected documentation and renewed confirmation first. Migrations, destructive operations, and live-data access need applicable authority and compatibility/recovery decisions; saved design is no substitute.

Documentation explains design; SQL, ORM, and migrations implement it. Keep them consistent. Synchronize later design changes first, and update any architecture links' version/scope. Added links/facts or implementation details preserving approved contracts do not automatically require reapproval or justify invented approval. Read-only diagnosis/review/planning and text/format-only maintenance do not trigger saving.

## Product Version Increments During Coding

This applies to all authorized project-code changes, including bug fixes and lightweight refactors, regardless of new features or release. Scope and counting units are in the [core standards](standards.md). Updating version metadata or correcting the same change does not recursively trigger another bump.

- Before editing, inspect the affected product/component's current version, authoritative source, and increment scheme, such as an existing `VERSION`, package manifest, or build configuration. Follow the project's increment level; an increment does not always mean a major-version bump. For multiple components, use established shared/independent versioning without upgrading unaffected Agents or other products.
- One complete change may span files and verification corrections. Before handoff, increment the actual source rather than only announcing a version or changing document/dependency versions. When resuming undelivered work, check the bump's baseline and record and reuse a correct existing increment. New edits after delivery require another increment.
- Use existing mechanisms to synchronize required package/build/display versions, lockfiles, and existing change records. Update only entries actually required to match, not every matching number across the repository or protocol/migration identifiers. Prefer project version tooling and structured parsers/existing tools for structured files. Do not run unauthorized commit/tag/release side effects bundled into a command.
- If the version source, initial version, or scheme is missing, or release-only repository versioning conflicts with this requirement, propose a minimal approach and ask the user to confirm affected decisions. Do not guess a baseline or redesign release workflows. A new project's first implementation records its confirmed initial product version; each subsequent code change increments it. Explain explicit prohibitions on version-file edits rather than writing without authority or claiming completion.
- Record old -> new versions, source locations, required synchronized entries, and the change summary in existing task/repair/change records and the final report, without a mandatory separate version ledger. Check the increment scheme, configuration parsing, and display/build consistency where actually inspectable. Disclose checks not run; see [verification and delivery](verification-and-delivery.md).

Pure documentation and read-only work do not bump the product version; code-file comment/format edits still count as code changes. Bumps add no requirements/architecture approval stage, grant no commit/tag/merge/release authority, and cannot justify breaking older-Agent compatibility.

## Work Breakdown and Change Control

- After both gates pass, break formal work down by requirements/modules. Localized repairs follow clear goals, scope, and verification. Each step has inspectable results; integration preserves buildability and testability.
- Protect existing behavior before large refactors, then split into reviewable changes. "Refactoring" is not permission to silently alter behavior.
- Explain acceptance, design, testing, and effort impacts of material requirements, stack, or boundary changes. Update affected documents and obtain approval before continuing, not after implementation.
- Implementation does not authorize deployment, production migrations, or external writes; a design proposal grants no execution authority.

## Interface and Data Changes

- Record new, changed, or deprecated public contracts and check known consumers. Do not silently alter defaults, error semantics, or field meanings.
- Changes to retries check idempotency, duplicate effects, and limits. Retries are not root-cause repairs.
- Migrations cover existing-data compatibility, order, verification, and recovery. If rollback is impossible, state a forward-repair strategy rather than promise nonexistent recovery.
- Separate temporary local tests from real-data operations. Use synthetic/sanitized data; destructive verification is confined to explicitly authorized isolated environments.

### Server and Agent Protocol Compatibility Design

Only for products with client Agent communication, following the [core standards](standards.md) redline:

- Record user/project version scope and source, and actual old requests, responses, interfaces, and workflows. Check presence, type, default, unit, enum, error semantics, and serialization; do not assume old parsers ignore new fields.
- Analyze direct/indirect Server effects including authentication, configuration, processing, and critical interactions. Cover applicable connection/registration, heartbeats, task exchange, result reporting, and other flows, not just unchanged endpoint names.
- Build a new-Server/older-Agent compatibility matrix with contract changes and preservation strategies. Adapters, dual protocols, or negotiation may fit the actual protocol; do not assume old Agents support new negotiation or require upgrades for existing workflows.
- Link the matrix to acceptance and test evidence. Requirements/design approval or an upgrade plan cannot replace compatibility verification or make breaking changes mergeable/releasable.

## Completion Conditions

Completion and stop conditions are defined in the [core standards](standards.md); actual evidence requirements are in [verification and delivery](verification-and-delivery.md). Retain the mode selected at the start, without reinstating exempted document requirements at handoff. Documentation can be delivered as a pending-approval draft, not claimed implementation.

Human approval, product acceptance, and post-release observation are separate states; AI self-review or passing tests cannot establish them.
