# Verification and Delivery

English translation | [Chinese rule source](../zh-CN/verification-and-delivery.md) | Paired revision: `2026-10-05.9`

Combine Google's effective testing/review principles, Microsoft's completion conditions, and AWS deployment-verification ideas. Risk determines check scope; not every task runs every check. See [sources.md](sources.md).

## Select Verification

For formal development, choose checks from approved acceptance criteria and module/interface contracts. Other modes check actual changes without blocking on missing product documents. Preserve traceability from requirements to owning modules and acceptance tests/checks; passing formal-development tests cannot compensate for unmet gates.

| Change | Evidence to consider |
| --- | --- |
| Text/comments/formatting | Diff review and format/parsing checks; explain why functional tests are unnecessary. |
| Defect repair | Original reproduction, post-fix regression tests, neighboring-behavior checks. |
| Feature/contract change | New behavior, boundary/failure cases, relevant type/build/consumer checks. |
| Database design/change | Actual structures, field semantics, constraints, and indexes match design; relevant access, compatibility, migration, recovery checks. |
| Server/Agent interaction | New Server with required older Agents: protocol, field semantics, core workflows. |
| Behavior-preserving refactoring | Behavior protection passing before/after, including errors and side effects; not just compilation, and no required failure on the old implementation. |
| Permissions/files/network/sensitive data | Allowed and denied paths, safe failure, no leakage or boundary escape. |
| Concurrency/resources/performance | Races, cancellation/cleanup, relevant load/performance evidence as applicable. |
| UI behavior | Actual runtime, key interactions, relevant viewports, errors, necessary visual checks. |
| Migration/deployment | Isolated rehearsal, compatibility, post-deploy health, recovery evidence. |

Reuse existing commands/frameworks. Do not install a whole toolchain merely because a tool is missing; choose a reasonable alternative or record the verification gap.

### Localized Repair Verification and Records

Localized repairs reduce documentation and repeat approval, not defect verification. Reuse or add regression cases that detect the original issue under clear intended behavior; check affected modules and necessary neighboring behavior. Do not duplicate tests or run unrelated whole-repository checks just to fill formalities. Establish scope/risk from actual calls, data flows, and contracts, not file count.

In the current task, existing Issue, or repair note, connect goals/evidence, actual code locations, and test/check commands/results. No new mapping table or requirements/architecture documents are mandatory; database-related coding still outputs/saves scoped design under the coding rule. Honestly mark necessary checks not run, blocked, or failed; do not claim complete verification. Formal gates and older-Agent evidence cannot be waived through this paragraph.

## Test Effectiveness

- Defect tests should fail on the old implementation and pass after repair. Run that comparison when safe; disclose when unavailable rather than invent earlier failure results.
- Check observable behavior/contracts, not merely implementation details. Choose interaction assertions according to risk.
- Do not let mocks hide the target issue. Fully mocked unit tests do not establish consequential cross-module/external-contract safety.
- Results are reproducible, failures understandable, and test data isolated; use synthetic or sanitized data.
- Coverage signals possible gaps, not correctness. Do not impose a universal 80% or 90% when the repository has no such gate.
- Rerun necessary checks after edits; earlier results cannot validate subsequent changes.

## Failure Handling

Record facts, causal hypotheses, and next checks. Use logs/diffs to narrow scope rather than endlessly repeating commands or expanding changes.

- **New regression**: Repair and verify again; do not hand off as passed.
- **Pre-existing failure**: Requires a baseline run or other evidence; otherwise mark the cause unconfirmed.
- **Environment blocker/not run**: Explain missing dependencies, authority, or services and resulting limits.
- **Not applicable**: Explain why unrelated; do not conceal verification gaps under this label.

Without sufficient evidence, hand off as "implemented, verification incomplete." Do not skip cases, remove valid assertions, disable checks globally, or turn off security controls to manufacture success.

## Code Self-Review

Review the complete diff and related call boundaries: consistency with applicable requirements/design or explicit repair goal/scope, responsibilities, necessary complexity, interface/error/resource clarity, effective tests, controlled security input flows, and updated relevant records.

Under [coding conventions](coding-conventions.md), check responsibilities and actual line counts for handwritten source files added/modified in this task. Use project thresholds, or assess files exceeding 1000 lines when none exist. Check reasonable splits or retention reasons and the provenance of generated/lockfile/third-party exemptions. After splitting, check calls/imports and behavior protection; shorter files do not prove preserved behavior. Disclose uncounted/unverified work without scanning/refactoring unrelated files or adding governance tools.

Self-review is not independent review. If another reviewer, CI, or product confirmation is required, mark pending approval rather than inventing it or bypassing gates.

## Interface Alternatives and Implementation Consistency

During design, actually open all three HTML visual prototypes in a browser and quickly check entry/asset loading, layout proportions, color/typography/spacing, component consistency, hierarchy, and readability/overflow/overlap at representative target viewports. Keep requirements/screens/data/viewports consistent with meaningful design differences, not wireframes, empty placeholders, or color swaps alone. Static HTML/CSS is sufficient: nonresponsive buttons or missing JS are not failures, and per-control interaction/end-to-end testing is not required by default. Check only scoped interaction demos explicitly requested by the user. Confirm no live business-service connections and record visual-only/unimplemented scope and actual rendering results. If browser access/authority is unavailable, report generated prototypes with rendering unverified, not invented visual-check success. Missing prototypes or authentic selection retain incomplete/pending-selection status.

After formal UI implementation, still compare actual layout, hierarchy, and key interactions with the selected option's version/scope. Run on target devices and retain necessary screenshots/evidence, checking applicable desktop/mobile viewports, text overflow/overlap, navigation, forms, key empty/loading/error states, and accessibility such as keyboard/focus behavior. Disclose unrun/unrendered checks; visual prototypes, old screenshots, and generated designs are not formal product verification. Attractive rendering or lightweight simulations prove no real service/database/permission behavior. Handoff links the selection, implementation, and actual results. Diagnosis alone grants no saved/edited design authority; actual product-code changes still require a product-version increment.

## Module and Acceptance Evidence

For formal development, update only current approved-scope evidence in an existing architecture mapping or linked acceptance record: requirement ID, owning module, actual code/test/check locations, implementation state, verification state, and results. With partial approval, retain other scopes as pending/unimplemented; passing one scope does not approve or accept the whole document. During design, record planned paths/checks, not implemented/passed status. No separate duplicate ledger is mandatory.

Record implementation and verification separately: implemented code with no tests run is "implemented / not run," not accepted. Distinguish passed, failed, not run, and not applicable; explain the latter two and their impact. Partial passing checks do not cover unverified acceptance criteria, and old-code results do not prove new changes.

Check actual calls/imports/data entrypoints against allowed dependencies, focusing on cycles, cross-layer access, and interface bypass. Reuse existing architecture/dependency checks. Without tooling, inspect relevant code/callers and record coverage; do not install a governance platform or call local review a full-repository validation. Required boundary/contract changes return to document updates and renewed approval.

Approval protects business/design content. Design-preserving code locations, results, or failure notes need no repeat approval and cannot silently enlarge approved scope.

## Database Design and Implementation Consistency

For database-related coding, check that relevant design essentials were output and accurate standalone documentation was saved/reused, identifying path, content version, and scope. Match actual SQL, ORM, migrations, and safely inspectable structures/constraints/indexes, updating architecture links when present. For existing databases, record current-design evidence and proposed differences, not assumptions as facts. Saved documentation or executable scripts do not prove design/acceptance passed. Verify affected access paths, rejected constraints, existing-data/consumer compatibility, and applicable migration/recovery; record actual commands, artifacts, and results. Disclose environment/authority gaps rather than accessing live databases or production data without authorization.

Synchronize design discrepancies and existing links. Implementation detail within approved scope adds no approval round; changes affecting requirements, stack, public contracts, module boundaries, or permission/data rules update and reconfirm affected content. Query repairs verify the original goal and also output/save relevant design, limited to current scope without whole-database or requirements/architecture backfill. Read-only checks grant no documentation-edit authority. Handoff includes relevant paths/versions, actual changes, and unverified work, not documentation completeness in place of checks.

## Product Version Handoff Checks

For project-code changes, compare with the pre-change baseline: the affected product's actual authoritative version must increment under the project scheme, with required package/build/display entries and existing change records consistent. A correct bump for the same undelivered change is not repeated for verification corrections or resumption. Chat announcements, document revisions, and dependency upgrades cannot replace an actual product-version change. Check structured configuration parsing and inspect runnable version output/build metadata through existing project mechanisms. Disclose unrun build/runtime checks rather than inventing consistency results.

Handoff includes old/new versions, source locations and required synchronized entries, a change summary, and actual check results. Without code changes, no product bump is needed. Report missing schemes, version-edit authority, or required synchronized entries without marking completion. A bump does not prove tests passed, approval, mergeability, or release; it neither waives bug regression/security/older-Agent verification nor authorizes tags or release.

## Older-Agent Compatibility Gate

For products with client Agent communication, Server changes affecting Agent interactions must follow the [core standards](standards.md) redline and established compatibility matrix, not just test the latest Agent:

- Record tested Server code/build, exact older-Agent versions and artifact provenance, environment, protocol/workflow scenarios, actual commands/cases/results, and evidence locations. Identify uncovered versions/flows; do not generalize one passing sample to all scope.
- Prefer real older-Agent/new-Server integration/end-to-end tests for agreed normal/failure flows. Cover relevant absent fields, defaults, types/enums, error responses, and old/new message parsing. Older Agents must still complete existing core workflows without upgrading.
- Historical protocol samples and contract tests supplement boundaries; sample replay, fully mocked units, and latest-Agent tests are not actual older-Agent end-to-end evidence. If sufficient protocol/core-flow compatibility proof is unavailable, state limitations and keep the gate unmet.
- Breaking compatibility, failing cases, missing evidence, or necessary checks not run block merge/release. Do not report "mergeable," "releasable," or verified compatibility. Hand off pending-review changes with specific blockers; forced Agent upgrades cannot remove the blocker.
- Merge/release also requires user authority and project approval/CI gates. Passing compatibility checks grants no execution authority. Do not change pipelines/deployment configuration merely because this rule exists.

Text-only changes or changes shown by impact analysis not to affect Agent interactions may mark this check not applicable with evidence. "Internal code only" or "one line" is insufficient. Link new-Server compatibility design/evidence to existing requirements/architecture records rather than duplicate ledgers. Qualifying repairs without historical product documents may keep scope, matrix, and actual evidence in the repair record, without backfilling two documents or skipping compatibility verification.

## Release Requirements

Execute only when the user explicitly includes release/migration and grants necessary authority. Ordinary coding reports release impact, not automatic deployment-configuration changes.

For production changes, establish success signals, observation window, failure triggers, and recovery; use existing small-batch/phased strategies. Data/protocol changes check old-version compatibility; code rollback is not proof of data recovery.

Automatic rollback, feature flags, alerts, and pipelines are optional implementation techniques according to project conditions. Without authority, provide pending steps rather than create production mechanisms.

## Evidence Handoff

Report only relevant facts: stage, goal/change outcome, actual check commands/results, consequential unverified work, compatibility/security/recovery risk, and required approvals or follow-ups. Formal development/product-document work includes document locations/versions and approval status. Localized repairs or behavior-preserving refactors give goal/evidence, scope, and checks without requiring two product documents; other lightweight/read-only work does not require them either. While awaiting approval, state implementation has not started. Implementation evidence should be locatable; do not output long checklists unsupported by real results.
