# development-standards User Guide

[简体中文](user-guide.zh-CN.md) | [Back to README](../README.md)

Applicable policy revision: `2026-10-05.9`. Written: 2026-10-05.

This guide is for product owners, non-technical users, and developers using an LLM to build software. It explains how to request work, approve decisions, and evaluate delivery. It adds no policy: [SKILL.md](../SKILL.md) and the [English standards](../references/en/standards.md) remain the execution references. Example versions, identifiers, and approval messages are illustrative, not authentic approvals for your project.

## Contents

1. [Quick Start](#1-quick-start)
2. [What to Provide](#2-what-to-provide)
3. [Choose the Appropriate Workflow](#3-choose-the-appropriate-workflow)
4. [A New Project from Discussion to Delivery](#4-a-new-project-from-discussion-to-delivery)
5. [Working on Existing Projects](#5-working-on-existing-projects)
6. [Approvals and Change Control](#6-approvals-and-change-control)
7. [Client and Server Products](#7-client-and-server-products)
8. [Evaluate the Handoff](#8-evaluate-the-handoff)
9. [Language, Resuming, and Sharing](#9-language-resuming-and-sharing)
10. [Frequently Asked Questions](#10-frequently-asked-questions)

## 1. Quick Start

Write `Use $development-standards` in the task message, followed by your goal and permitted actions. Codex supports explicit skill selection and can also select by task/description. CLI/IDE users can use `/skills` or `$`; UI entry points vary. Naming the skill in your request does not depend on a particular button. See the [official OpenAI skills documentation](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills).

For a new project:

```text
Use $development-standards to build a local task management tool.
I am the only user, primarily on a computer. Accounts and cloud sync are out of scope.
I am not technical. Discuss requirements with me in English and write the requirements document.
After requirements approval, offer viable stack options with a recommendation,
then discuss modules and architecture.
Do not scaffold or write formal code/tests until the applicable requirements,
stack, and complete design approvals are in place.
This task does not authorize commits, pushes, deployment, or paid resources.
```

You need not read every standard or choose a framework first. Describe the problem and constraints; the model should ask focused questions in stages.

The skill guides model behavior; it is not a runtime interceptor. Explicit invocation clarifies intent but does not guarantee correct selection or execution. Inspect the documents, code, and verification evidence.

## 2. What to Provide

Provide what you know. Mark unknowns for discussion rather than inventing answers.

| Information | What to describe |
| --- | --- |
| Goal and users | Who uses it, what problem they face, and what useful success looks like. |
| Scope and non-goals | What this iteration must include and what should wait. |
| Project location and state | New or existing project; working directory, relevant modules, documents, or Issue. |
| Runtime and maintenance | Computer/browser/phone, connectivity, deployment constraints, budget, and maintainer. |
| Known stack and conventions | Specified technologies, repository rules, existing test commands; note if absent. |
| Acceptance and preserved behavior | Example inputs/outputs, errors, existing interfaces, compatibility requirements. |
| Authorization | Discussion or diagnosis only, or permitted edits; any separately scoped release/data work. |

Use synthetic or redacted examples, not real secrets, personal information, or production data in prompts. Clarify scope and safe access before work needs external services, additional permissions, or live environments.

The runtime must discover the complete skill folder, not just `SKILL.md`. In this project's maintenance environment it is installed at `~/.codex/skills/development-standards`. That is the observed local location, not a universal discovery path for every Codex version. For other environments, use the [official local discovery documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) and actual runtime configuration. This guide does not require moving an existing installation.

## 3. Choose the Appropriate Workflow

The model should inspect relevant code, callers, data flows, and project rules. Line counts, file counts, and task labels alone do not determine the workflow.

| Requested work | Workflow | Main user decisions |
| --- | --- | --- |
| Explain, diagnose, review, or plan | Read-only | Goal and scope; missing product documents do not block inspection, and no edits are implied. |
| Write or revise requirements, design, or standards | Documentation | Content and status; pending drafts are valid deliverables, without incidental implementation. |
| Text, formatting, mechanical edits, or qualifying behavior-preserving refactors | Lightweight maintenance | Edit authorization, scope, and verification; no historical product-document backfill. |
| Restore clear existing intended behavior within low risk | Localized repair | Expected behavior, evidence, scope, and repair authorization; no redundant requirements/design approval. |
| New project, feature, interface change, or non-qualifying repair/refactor | Formal development | Requirements first, then complete design for this scope; explicit stack approval for new projects. |

Lightweight paths reduce documentation and repeated approval, not verification, security, or compatibility obligations. Authorization, sensitive data, migrations, concurrency/resource lifetimes, and production changes are not exempt because a change is small or called a refactor.

When scope or risk increases, stop the affected work, explain why, and use the applicable workflow. Independent, clearly authorized safe work may continue. Stricter user or project requirements still apply.

## 4. A New Project from Discussion to Delivery

```text
Requirements discussion -> Requirements document -> User approval
-> Stack and module/architecture discussion -> Architecture document -> User approval
-> Implement approved scope -> Verify -> Handoff
```

### 4.1 Discuss and Approve Requirements

The model clarifies goals, workflows, scope, business rules, inputs/outputs, failure cases, constraints, and acceptance. The default document is `docs/requirements.md`; existing repository locations and formats take precedence.

Check these points:

- Scenarios match real use, without unrequested features.
- Acceptance is observable and testable, not just "works correctly."
- Unknowns are pending decisions; scope and non-goals are explicit.
- Preserved behavior, permissions, data, and compatibility requirements are covered.

Request revisions first when needed. Once satisfied, you can say:

```text
I approve docs/requirements.md v1 for REQ-001, local task creation.
REQ-002, search, remains unapproved and outside this implementation.
Proceed to stack and architecture discussion based on these requirements.
Do not write formal code yet.
```

This is a clear example, not a mandatory phrase. Approval must identify the content version and scope. Before requirements approval, discussion, requirements edits, and read-only research can continue; formal architecture and implementation should not.

### 4.2 Select a Technology Stack

Non-technical users can describe practical constraints and ask for understandable trade-offs:

```text
I want single-user operation, easy installation, local data storage,
and straightforward maintenance.
Compare genuinely viable options and identify a recommendation.
Explain deployment, operating cost, maintenance, and limitations before technical names.
Clearly mark estimates and unverified prices, versions, or maintenance status.
```

Typically compare 2-3 viable combinations, not a list of unfamiliar dependencies. Preserve specified technologies; do not manufacture options when only one fits. A model recommendation is not your approval.

Record the stack in the architecture document, not a mandatory third document. Approve it separately or together with a complete architecture that clearly states it. Stack approval alone does not approve the complete design, purchase services, or authorize deployment.

### 4.3 Review Modules and Architecture

The default is `docs/architecture.md`, linked to approved requirements. You need not inspect every code line to understand what each module does, how modules cooperate, and what happens on failure.

| Check | Questions to ask |
| --- | --- |
| Responsibilities | Who owns UI, business rules, and storage? What is outside each module's responsibility? |
| Interfaces and data | How do inputs, results, and errors cross boundaries? Who owns and may access data? |
| Key flows | Is the sequence from user action through processing, persistence, and response complete? |
| Complex-module/workflow diagrams | Do complex modules have architecture diagrams and complex workflows have flowcharts? Do boundaries, dependencies, branches, and failures match the text? |
| Necessary dependencies | Are required shared rules/components explicit and approved? |
| Security and failures | Are applicable permissions, failure handling, resource cleanup, and recovery explained? |
| Acceptance mapping | Who implements each scoped requirement, and how is it checked? Are planned paths distinguished from implementation? |

A directory tree or list of frameworks is not module design. Small projects can stay simple; do not add microservices, databases, or layers just to fill a template.

For new interfaces or material redesign, the model must first deliver **three HTML visual prototypes/mockup pages** for you to view in a browser and choose. They share requirements, representative screens, sample data, and viewports, comparing layout, density, hierarchy, and consequential trade-offs. Focus on aesthetics, color, typography, spacing, component styling, and content organization appropriate to the product. **Static HTML/CSS is sufficient; complete interactivity, JS, button responses, form validation, and business flows are not required by default.** Explicitly scope particular demos when needed, rather than building three complete products during selection. Text, images, empty wireframes, or color swaps alone are insufficient. Provide actual file links or a local preview URL when necessary, explaining visual-only/unimplemented scope and actual rendering-check results without live business-service connections. Select one or request a combination; view and confirm the revised result. Save entries, option versions/scope, and authentic selection in design documentation. Selection may accompany architecture approval but neither approves all architecture, authorizes product coding, nor proves functional completion.

```text
First provide three browser-openable HTML visual mockup pages, A/B/C, for the same screens and sample data.
Prioritize aesthetics, layout, color, typography, spacing, and hierarchy. Static HTML/CSS is sufficient; complete interactivity is unnecessary.
Explain visual differences, your recommendation, actual rendering checks, and unimplemented scope; provide each entry.
After I view and select one, implement approved scope only; prototypes use no live services and are not completed products.
```

Reuse clear valid applicable selections. Implementing an established design or repairing its bugs/text does not force reselection; actual redesign or an explicit current request for three still requires alternatives. Read-only reviews and products without UI do not authorize new design files/interfaces. Disclose unavailable preview tools rather than claiming shown results. See the [engineering workflow](../references/en/engineering-workflow.md).

Complex modules, such as layered responsibilities, cross-dependencies, or multiple external participants, require architecture diagrams explaining components, boundaries, and relationships. Complex workflows, such as branching, async/concurrent work, retry/compensation, or state transitions, require flowcharts explaining steps, conditions, results, and key failure paths. Save diagrams with architecture using project formats or editable inline Mermaid when unspecified. Sequence/state diagrams may supplement but not replace required flowcharts. Complete them before architecture approval; placeholders or spoken/chat descriptions are insufficient, and no separate diagram approval is added. Simple clear designs may use text/tables; read-only/lightweight tasks do not backfill whole-project diagrams.

Architecture still addresses storage selection, data ownership, and key contracts, without requiring detailed database design as an approval attachment. Database design output belongs to the next section's coding-start check.

An approval example:

```text
I approve docs/architecture.md A1 based on requirements v1, REQ-001.
This includes its explicit option A stack, the complete scoped module design,
data contracts, and necessary shared dependencies.
REQ-002 remains pending and must not be implemented.
Implement and verify REQ-001 within the workspace.
Commits, pushes, and deployment are not authorized by this task.
```

"Option A" must refer to a concrete proposal you have reviewed, not an undefined name. Before applicable gates pass, do not scaffold, install project dependencies, or write formal code/tests. A feasibility experiment needs separate scoped authorization and isolation; it does not replace design approval.

### 4.4 Implement, Verify, and Deliver

Implement approved scope only, reuse project conventions/frameworks/mature libraries, and apply relevant Tencent-derived security guidance. If requirements, the stack, public contracts, or module boundaries must materially change, update affected documents and obtain approval before that implementation, not afterward.

During coding, each handwritten source file must have a single, clear responsibility, not mix independent modules. Project file-length conventions take precedence. Without them, files added/modified in this task that exceed **1000 lines require split assessment**, counting all physical lines including blanks/comments by default. This is an assessment threshold, not a hard cap; mixed responsibilities still matter below it. Split by responsibilities/dependencies, not mechanical chunks, code compression, or removal of meaningful comments to meet a number.

When retention is necessary, the model explains paths, actual counts, responsibility assessment, reasons, and follow-up recommendations without mandatory new documents/approval. Verifiable generated code, lockfiles, and third-party code are exempt from the default threshold. Do not refactor unrelated legacy files. Splits exceeding authority or changing contracts/module boundaries require applicable confirmation first. Read-only reviews only report, and text/format-only maintenance does not automatically authorize splitting. See [coding conventions](../references/en/coding-conventions.md).

At coding start, the model must check whether scoped work uses a database. If so, output design essentials and save a standalone document before database-related queries, SQL, ORM, or migration code, defaulting to `docs/database-design.md`. Without a database, skip it rather than creating an empty document or adding storage to fill a template. The [database design template](../assets/en/database-design-template.md) covers relevant entities/relationships, fields/constraints, access/indexes, ownership, and applicable transactions, compatibility/migrations, and verification.

Propose design for a new database. For an existing one, first inspect relevant schema, ORM, migrations, and documentation, explaining current/proposed differences. Reference accurate unchanged documentation with path/version and essentials. Update changed design or document only missing current scope, not the entire history. SQL, ORM, or migrations alone cannot replace explanations, and the rule grants no production-database access.

This is a coding deliverable, not an advance architecture document/approval or separate database approval stage. Implementation details within approved scope may proceed. Changes affecting approved requirements, stack, public contracts, module boundaries, or permission/data rules still need affected confirmation; actual migrations/destructive operations retain separate task authority. Database query repairs/refactors also output relevant scoped design without requirements/architecture backfill. Explicit prohibitions on document edits must be resolved rather than bypassed. Read-only diagnosis/review/planning and text/format-only work do not trigger saving.

Every complete code change, including bug fixes, refactors, code comments/formatting, and test/script edits, increments the affected product version even on lightweight paths. Files and verification corrections within one change share one increment; new edits after delivery need another. Inspect the actual project version source/scheme and synchronize required entries before handoff. A new project's first implementation uses the initial version confirmed with you. Missing rules or prohibited version-file edits require explanation and confirmation, not invented versions. Pure documentation and read-only tasks do not bump the product version. Bumps grant no commit/tag/merge/release authority and do not replace older-Agent verification. See the [engineering workflow](../references/en/engineering-workflow.md).

The handoff should link requirements to actual modules, code, and checks, not just announce completion. You can request:

```text
Report implementation locations and actual acceptance results for approved scope.
For over-threshold handwritten source files, report actual counts and split outcomes or retention reasons.
For code edits, report old -> new product versions, the actual source, and required synchronized entries.
List commands run, passed/failed results, and key unrun checks with reasons.
Separate implemented, verified, approved, and deployed states.
Do not describe self-review as independent review.
```

## 5. Working on Existing Projects

### 5.1 Diagnose Without Edits

```text
Use $development-standards to diagnose the export failure.
Inspect relevant code, callers, configuration, and tests without modifying them.
Explain the evidence and propose a repair.
Do not edit code, tests, documents, or deployment configuration.
```

Finding a problem does not authorize fixing it. Explicitly request a repair afterward when ready.

### 5.2 Authorize a Localized Repair

```text
Use $development-standards to fix label display.
Trim boundary ASCII spaces only; preserve internal spaces, case, and other whitespace.
Authorize the localized repair and related regression tests, not an original-text
viewer or public contract changes.
First establish low risk, then briefly state evidence, scope, and verification.
If qualified, do not backfill historical requirements/architecture documents.
Explain and ask if intent is unclear or scope must expand.
```

Reuse effective tests. Defect regression should detect the old problem; safely run old-fails/new-passes verification when possible. Disclose inability to replay rather than fabricate results. Multiple existing modules do not automatically disqualify a repair, but responsibilities, dependencies, contracts, and bounded risk must still be preserved and verified.

### 5.3 Preserve Behavior During Refactoring

```text
Use $development-standards to remove duplicate formatting logic within one module.
Authorize a private helper extraction, preserving inputs/outputs, errors,
side effects, and call order.
Do not change business rules, stack, public contracts, module responsibilities,
or dependency direction.
Inspect actual callers and risk first. If qualified, use lightweight maintenance
and compare behavior before and after.
If authorization, sensitive data, migrations, or other high risk is discovered,
stop the affected implementation and explain the next step.
```

Behavior-protection tests should pass before and after a behavior-preserving refactor; no manufactured old-implementation failure is needed. A small authorization-helper extraction still touches high risk and does not qualify for this exemption.

### 5.4 Add Features or Change Interfaces

```text
Use $development-standards to add search to the existing tool.
Check whether existing requirements, design, stack, and authentic approvals
cover this scope. Reuse valid baselines.
Document and approve only the affected uncovered requirements and design.
Do not implement before applicable approval or incidentally reselect the stack
or refactor unrelated modules.
```

Do not repeatedly request valid approvals. Missing formal-development baselines require documentation for this scope, not rewriting the whole product's history.

## 6. Approvals and Change Control

"Build it" or "recommend something" is not approval of a later requirements or stack draft. Natural language is sufficient when the context is clear. Identifying the document, content version, scope, and pending items helps future continuation.

| Situation | Correct handling |
| --- | --- |
| Requirements only approved | Discuss stack/design, without implementation. |
| Stack only approved | Complete and approve the scoped design before implementation. |
| Only independent REQ-001 approved | Implement once its requirements, complete design, and necessary dependencies are approved; unrelated pending REQ-002 does not block it. |
| Required shared contract undecided | Approval of the goal alone does not unblock dependent implementation. |
| Document says "approved," source unverifiable | Ask the user to approve current content; do not invent history. |
| Material requirements, acceptance, stack, or boundary changes | Update affected documents, invalidate affected approvals, and reapprove before continuing affected implementation. |
| Spelling, formatting, approval metadata, or evidence-only updates | No automatic reapproval, and no expansion of approved scope. |

Requirements changes affect designs depending on them. Design-only changes should not invalidate unrelated requirements without reason. Keep mixed status by scope; partial approval is not whole-document approval or acceptance.

Completing the task does not expand authority to commit, push, create PRs, merge, release, migrate production data, or write externally. Those actions must fall within your authorization and project gates.

## 7. Client and Server Products

An Agent here is the product's software client or collector, not an LLM. Server upgrades/changes must preserve protocols, interfaces, field semantics, and core workflows for older Agents within the defined compatibility scope. Agent upgrades cannot be a prerequisite for existing workflows to keep working.

Provide or discuss the user/project-defined version range and basis, protocol baseline, required workflows, available older-Agent artifacts, isolated environment, and evidence location. The model must ask when scope is unclear, not retire older versions itself.

```text
Use $development-standards to change Server result reporting.
Check the project's older-Agent compatibility scope and protocol baseline first;
ask about unclear decisions.
Preserve existing core workflows without upgrading older Agents.
Record actual Server/Agent versions, scenarios, commands, results, and evidence.
Latest-Agent tests, historical replay, or fully mocked checks must not be called
real older-Agent end-to-end verification.
Incompatibility, failed/unrun required verification, or missing evidence keeps
the relevant merge/release gate unmet.
This task does not authorize merge or release.
```

Requirements/design approval does not waive this redline. Passing compatibility tests does not authorize release. Without sufficient evidence, deliver a reviewable patch with blockers, not a claim of verified compatibility or merge/release readiness. A qualified repair may record compatibility in its repair note without historical document backfill, but still needs verification.

## 8. Evaluate the Handoff

Evaluate according to task mode and risk, not a mandatory full checklist on every task. Understand the current stage, actual changes, relevant checks, and unresolved work.

| State | Means | Does not mean |
| --- | --- | --- |
| Approved | Authentic approval of a content version and scope. | Implemented, tested, or deployment authorized. |
| Implemented | Target code has been changed or created. | Acceptance/security checks passed. |
| Verified | Relevant checks on the corresponding change actually passed. | Every scenario covered, independent review, or release complete. |
| Deployed | Actual deployment execution and results are evidenced. | All business, security, or compatibility goals automatically met. |

Look for passed, failed, not run, and not applicable checks. Partial passing results do not cover unverified acceptance. Unexplained failures cannot simply be labeled pre-existing. Without a usable environment, report "implemented, verification incomplete," not success manufactured by skipping tests or disabling authorization/security controls.

For formal work, inspect the requirement/module/code/acceptance mapping. For repairs/refactors, inspect evidence, scope, and checks without demanding exempted product documents. Model self-review cannot replace required independent review, human approval, or CI gates.

## 9. Language, Resuming, and Sharing

Use the same `$development-standards` in either language; two installations are unnecessary. An explicit instruction-language preference takes precedence. Otherwise Chinese requests use Chinese resources, English requests use English resources; other languages use English resources and communicate in the user's language.

Document language can differ from conversation: explicit document language first, existing repository convention second, conversation language last.

```text
Use $development-standards. Discuss in English, but write requirements and
architecture documents in Chinese. Preserve code identifiers and unrelated files.
```

When resuming, provide the project location, approved versions/scope, verifiable sources, completed work, and blockers. The model should check that content and approvals still correspond. If prior approval cannot be verified, you may approve the current version rather than recover lost conversations. Language switching alone does not invalidate approvals or authorize new work.

```text
Continue using $development-standards.
Check whether existing requirements, architecture, and approvals cover the current
scope, then continue clearly approved safe work.
Do not treat an "approved" label or old test result as current approval/verification.
```

Share the complete skill folder, including both language trees, templates, UI configuration, and attribution. This manual is for people, not an additional mandatory model read. Maintain Chinese sources and English translations together for policy/template changes. Do not silently select weaker translations; follow entrypoint maintenance rules.

## 10. Frequently Asked Questions

**Why did the model stop during discussion?**

Check whether requirements, complete design, stack, or necessary dependencies affecting current scope remain unapproved. Staying at the appropriate stage is part of formal development; discussion and document revision can continue. Qualified repair/maintenance should not be blocked only by missing historical documents.

**It demands two documents for a small bug. What should I do?**

Ask it to explain classification using actual calls, data flows, contracts, and risk. Qualified localized repairs need no backfill. Permissions, data safety, or changed contracts can prevent exemption even for a small patch.

**Can the model choose technologies?**

Ask for a reasoned recommendation, then approve the concrete proposal. Preserve technologies already specified and discuss only remaining important choices, not every transitive dependency.

**The skill is installed but not selected, or the wrong version is loaded.**

Explicitly invoke it and request the actual `SKILL.md` path and paired revision. Check directory completeness, disabling configuration, and same-named copies. Official documentation states that same-named skills are not merged and that restarting can help when updates do not appear; see [local skill documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills). Do not start troubleshooting by overwriting installs or changing global configuration.

**Can I approve everything at once?**

Approval must identify actual discussed content and scope, not future drafts. Approve requirements first, then discuss and approve the complete design. The stack can be approved with a design that explicitly includes it. Reuse authentic, valid, applicable approvals.

**Does the guide guarantee no unauthorized actions or missed tests?**

No. The skill stays lightweight and model-led. It does not replace a sandbox, access controls, CI, security scans, or human review. Judge actual artifacts and evidence, not only assertions of compliance.

## Rules and Templates

- [Entrypoint](../SKILL.md): language selection, shared constraints, and maintenance.
- [Core standards](../references/en/standards.md): task modes and lightweight eligibility.
- [Engineering workflow](../references/en/engineering-workflow.md): discussion, stack, approvals, and change control.
- [Coding conventions](../references/en/coding-conventions.md) and [Tencent security](../references/en/tencent-security.md): project-first implementation and applicable safety checks.
- [Verification and delivery](../references/en/verification-and-delivery.md): tests, compatibility evidence, and handoff states.
- [Requirements template](../assets/en/requirements-template.md) and [architecture template](../assets/en/architecture-template.md): adapt when formal development needs documents.
- [Database design template](../assets/en/database-design-template.md): output/save during database-related coding; propose new design or inspect/reuse/update existing design.
- [Sources and limitations](../references/en/sources.md): attribution and adaptations, not an official unified company policy.
