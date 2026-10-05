# Database Design

English translation | [Chinese template source](../zh-CN/database-design-template.md) | Paired revision: `2026-10-05.9`

Applicability: coding involving a database, including new databases, existing-database implementation, query repairs, and refactors. No database, text/format-only maintenance, and read-only work do not trigger saving; read-only work does not authorize copying/filling this template.

Usage: at coding start, present scoped design essentials and save before database-related code; default to `docs/database-design.md`. No advance database document during architecture or separate database approval is required. For existing databases, inspect relevant schema, ORM, migrations, and documentation. Reference accurate unchanged documentation and its essentials; update changes or document only missing current scope. Adapt to the actual model/risk; remove inapplicable sections and explain important exclusions. Do not invent database capabilities, performance metrics, or migration recovery. SQL, ORM, and migration scripts alone do not replace this document.

## State, Scope, and Design Basis

- Document identity/path, current content version, requirement/module scope; distinguish current design, non-goals, and existing/planned state.
- Related requirements/architecture and their actual approved scope, when available; localized repairs do not backfill those documents for this template.
- Evidence for current design: relevant schema, ORM, migrations, or existing design records/locations; identify discrepancies and unknowns.
- Actual state: existing design, planned, in progress, implemented, and verification state; no default approval wait.
- Open issues/blockers. Changes affecting approved requirements, stack, public contracts, module boundaries, or permission/data rules identify affected content and authentic confirmation sources before implementation.

This template needs no separate approval. Implementation detail within approved scope does not automatically require reapproval or justify calling unapproved details approved. Live-data access, migrations, and destructive operations still need applicable authority; file existence proves neither verification nor permission to operate.

## Database and Design Boundary

Link actual or approved storage choices and applicable versions. Describe database/namespace, owning modules, data purpose, and scope. Distinguish existing/new design and do not switch stacks on your own. Do not duplicate stack-choice ledgers or record real credentials/production data.

## Entities and Relationships

| Entity/table/collection | Business purpose | Owning module | Identifier/key | Relationships, cardinality, delete/update rules | Existing/planned |
| --- | --- | --- | --- | --- | --- |

Explain complex relationships with diagrams or text. Distinguish database constraints from application guarantees according to actual capabilities; not all stores support foreign keys or transactions.

## Fields and Integrity Constraints

Record fields per entity, or field paths for nested documents. Explain complex rules in separate sections.

| Entity/field | Business meaning | Type/precision/unit | Nullability/default | Unique/reference/validation constraints | Compatibility/existing-data impact |
| --- | --- | --- | --- | --- | --- |

Explain relevant identifiers, enums, time/timezone, and ordering/collation rules. Same-named fields need not share meaning. Distinguish facts, planned choices, and unresolved issues.

## Access Paths, Indexes, and Trade-Offs

| Query/access scenario | Filtering, ordering, joins | Index, field order/uniqueness | Rationale/write cost | Planned checks/actual results |
| --- | --- | --- | --- | --- |

Connect indexes to actual access needs; state when no new index is needed. Record relevant query plans or isolated tests without claiming planned performance is verified.

## Ownership, Access, and Consistency

Describe module read/write entrypoints, permissions/isolation, applicable sensitive-data retention/deletion, and transaction/concurrency/consistency boundaries. Match architecture contracts; design documentation grants no live-data access authority.

## Changes, Migration, and Recovery (When Applicable)

Describe current/target structural or semantic differences, compatibility, migration order or planned/actual script locations, prerequisites, existing-data handling, failure criteria, and feasible recovery. If rollback is unavailable, explain forward repair or another viable strategy. Code rollback does not guarantee data recovery. Distinguish a new empty database from migration of existing data.

Actual migration/destructive testing requires separately scoped authority and isolation; design approval does not authorize production operations.

## Verification and Implementation Links

| Requirement/design item | Owning module | Planned/actual SQL/ORM/migration location | Structure, constraint, access, compatibility checks | Implementation state | Verification state/evidence |
| --- | --- | --- | --- | --- | --- |

During design, mark planned/not run. After implementation, check actual structures/code/migrations against this document and record real commands/results/evidence. Disclose failed or missing necessary checks; complete documentation does not establish implementation correctness.

## Open Issues and Change Record

Record questions, impact, current-scope blockers, and resolution. Track current/proposed differences, versions/scope, and actual state of necessary decisions. Explicitly identify no blockers; future-iteration issues stay outside current scope.
