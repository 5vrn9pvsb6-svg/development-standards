# Coding Conventions

English translation | [Chinese rule source](../zh-CN/coding-conventions.md) | Paired revision: `2026-10-05.9`

## Select Rules

Priority: explicit repository standards/tool configuration, neighboring code and existing framework patterns, then applicable public references. Do not simultaneously apply conflicting Google, Airbnb, or company rules.

| Technology | Reference when local conventions are absent | Limitations |
| --- | --- | --- |
| Python | PEP 8, Google Python Style Guide | Preserve compatibility, not formatting at its expense; check syntax/APIs against the actual runtime. |
| Go | Google Go, Uber Go Style Guide | Preserve idiomatic Go; do not copy obsolete tooling recommendations. |
| Java | Google Java, Alibaba Java manual | Select rules for the actual Java version and framework. |
| JavaScript / TypeScript / React / Node.js | Alibaba frontend conventions; Airbnb as an alternative | Do not mix whole style systems; check framework/lint compatibility. |
| C / C++ | Existing project standards; Google C++ as a supplement | Project contracts govern exception, memory, and ABI policies. |
| C# / .NET | Project `.editorconfig`; Microsoft C# conventions | Microsoft example, runtime, and compiler projects do not use identical rules. |
| REST API | Microsoft Azure REST API Guidelines | Use contract design principles, not mandatory Azure paths, version parameters, or internal approval flows. |

See [sources.md](sources.md) for links. Check official documentation only when needed for the task and local evidence is insufficient; do not introduce new formatters automatically.

## Cross-Language Quality

- Names convey purpose, units, and business meaning; avoid vague `data`, `temp`, or `util` as primary interface semantics.
- Give functions, modules, and files clear responsibilities. Reduce nesting and clarify conditions in complex branches; assess file length under the rules below, not as a substitute for responsibility and maintainability judgments.
- Public interfaces define types/structure, error semantics, and side effects. Do not pile repetitive documentation onto every internal function.
- Separate data from instructions: parsers for structured data, parameter binding for queries, explicit programs/argument arrays for system commands.
- Preserve module boundaries and dependency direction; explain benefits and maintenance costs of abstractions, caches, concurrency, and dependencies individually.
- Release resources according to explicit lifetimes; async tasks support cancellation and waiting. Preserve useful error context without duplicate handling or secret disclosure.
- Do not ignore return values, cancellation, or Promise failures, or treat empty collections/defaults as a universal exception handler.
- External documentation describes contracts; internal comments explain non-obvious reasons. Update relevant explanations when code changes.

## Clear Modules and File Length

- Each handwritten source file must have a single, clear responsibility, organized around one cohesive purpose. Do not pile independent modules or unrelated business responsibilities into one file. Mixed responsibilities require a reasonable split assessment even below the length threshold.
- Follow explicit project file-length or splitting conventions first. Without them, use **1000 lines as the split-assessment threshold**. A handwritten source file added or modified in this task that exceeds 1000 lines requires assessment; do not keep adding code without explanation. This is not a hard cap. Exactly 1000 lines does not trigger assessment by length alone.
- By default count all physical lines, including blank lines and comments, or follow the project's counting convention. Do not compress statements, remove meaningful comments, or change formatting to evade assessment. Without actual counting, do not claim length was checked.
- Split by business responsibilities, cohesion, interfaces, and dependencies, not fixed-size chunks. Split when reasonable boundaries and safe separation exist within current authority, preserving behavior, errors, side effects, and dependency direction. Do not create fragmented files, cycles, or meaningless forwarding layers.
- When retaining an over-threshold file is necessary, record its path, actual line count, responsibility assessment, retention reasons, and follow-up recommendations in the current task, an existing maintenance record, or handoff. No new document or approval stage is mandatory. If splitting exceeds authority, changes public contracts/module boundaries, or introduces high risk, clarify or obtain applicable approval first; file length grants no expanded authority.
- Generated code, lockfiles, and third-party/vendor code are exempt from the default threshold. Do not edit generated outputs merely to satisfy it. Exemptions need verifiable provenance; handwritten code cannot exempt itself by filename alone. Assess only affected files, not unrelated whole-project refactoring of existing large files. Read-only reviews only report; text/format-only maintenance does not automatically authorize structural splitting.

## Automated Checks

- Use existing format, lint, typecheck, compile, and test commands; check whether they modify files or cause external effects.
- Format only current scope unless the user explicitly requests whole-repository formatting.
- Explain new rule exemptions, preferably scoped to specific code. Do not disable a whole rule or weaken global checks merely to remove errors.
- Naming, line width, coverage, and dependency counts alone do not guarantee quality. Do not turn a company's numeric examples into automatic project gates.
