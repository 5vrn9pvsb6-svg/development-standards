# Sources and Applicability Limits

English translation | [Chinese rule source](../zh-CN/sources.md) | Paired revision: `2026-10-05.9`

Source compilation/review date: 2026-10-03. Official public links point to changing pages, not guaranteed fixed versions. This skill is an original operational synthesis, not copied manuals, official certification, or a company's internal policy.

Separate requirements and complete current-scope design discussion, documentation, and user approval before formal implementation are user-defined gates. Lightweight paths for clear, verifiably scoped low-risk localized repairs and behavior-preserving refactors without historical product-document backfill are also user-selected policies. Templates, module mapping, and maintenance records are supporting adaptations, not a company's original or universal procedure.

New-project stack confirmation and understandable viable options for non-technical users are user-defined workflow requirements. Comparison, records, and stack-change approval are supporting adaptations, not attributed to a company's public policy.

The older product Agent compatibility redline is also a user-defined product constraint, not attributed to Tencent security guidance or another company's policy. Protocol design and evidence requirements support that constraint.

The single-entrypoint bilingual layout, language selection, Chinese source of truth, and paired translation maintenance are user-selected skill conventions, not a company's engineering policy.

Checking database use at coding start and outputting/saving scoped standalone design is also user-defined: propose new databases, inspect/reuse/update existing design, and skip when no database is used. The document belongs to coding, not an architecture-approval prerequisite or separate approval stage. Templates, document/implementation consistency, scope-change handling, and read-only boundaries are supporting adaptations, not attributed to a company's public policy.

Requiring architecture diagrams for complex modules and flowcharts for complex workflows during architecture design is also user-defined. Complexity criteria, saved artifacts/consistency checks, and simple/lightweight/read-only boundaries are supporting adaptations, not a company's universal diagram policy or an additional approval stage.

Incrementing the product version for every project-code change, including bug fixes, is also user-defined, not a company's universal policy. Complete-change counting, actual version sources/synchronization, avoiding duplicate bumps on resumption, and read-only/release authority boundaries are supporting adaptations. Product versions are distinct from skill paired revisions or project document content versions.

Providing three browser-viewable HTML visual prototypes emphasizing aesthetics and visual quality is a user-defined, revised requirement, not a company's universal policy. Static HTML/CSS mockup pages are sufficient; JS/interactions are optional by default, with explicitly requested scoped demos only, reducing design-stage cost. Actual rendering checks, same-scope comparisons, design records/authentic selection, reuse of valid decisions, and read-only/prototype boundaries are supporting adaptations. Standalone images/text cannot replace HTML entries. Visual prototypes do not prove functional completion, authorize premature product implementation/live services, or add a fixed approval ledger.

Clear module/handwritten-file responsibilities and a 1000-line split-assessment threshold when project length conventions are absent are user-selected coding constraints, not a universal company cap. Physical-line counting, responsibility-based splitting, retention reasons, generated/lockfile/third-party exemptions, and task-scope boundaries are supporting adaptations. Exceeding the threshold requires assessment, not automatic prohibition or authority for unrelated refactoring.

## Engineering Process and Quality

- [Microsoft ISE Engineering Fundamentals Playbook](https://microsoft.github.io/code-with-engineering-playbook/): process reference. Its [Ready](https://microsoft.github.io/code-with-engineering-playbook/agile-development/team-agreements/definition-of-ready/), [Done](https://microsoft.github.io/code-with-engineering-playbook/agile-development/team-agreements/definition-of-done/), [design template](https://microsoft.github.io/code-with-engineering-playbook/design/design-reviews/recipes/templates/feature-story-design-review/), and [engineering checklist](https://microsoft.github.io/code-with-engineering-playbook/engineering-fundamentals-checklist/) inform requirements/design/completion. Example coverage, reviewer counts, and organizational roles are not adopted automatically.
- [Google Engineering Practices](https://google.github.io/eng-practices/review/reviewer/looking-for.html), [Small CLs](https://google.github.io/eng-practices/review/developer/small-cls.html): self-review dimensions and focused changes.
- [Software Engineering at Google](https://abseil.io/resources/swe-book/html/toc.html): maintenance context; [rules](https://abseil.io/resources/swe-book/html/ch08.html) and [unit testing](https://abseil.io/resources/swe-book/html/ch12.html) support reader-first code and effective tests.
- [GitLab development workflow](https://docs.gitlab.com/development/contributing/merge_request_workflow/): submission, acceptance, and post-release responsibility references, not universal product-specific acceptance rules.
- [AWS automated testing and rollback](https://docs.aws.amazon.com/wellarchitected/latest/framework/ops_mit_deploy_risks_auto_testing_and_rollback.html): production success/failure signals and recovery; no AWS integration requirement.

## Coding Conventions

- [Google Style Guides](https://google.github.io/styleguide/); [Python](https://google.github.io/styleguide/pyguide.html), [Go](https://google.github.io/styleguide/go/), [Java](https://google.github.io/styleguide/javaguide.html), [C++](https://google.github.io/styleguide/cppguide.html). Project conventions take precedence.
- [PEP 8](https://peps.python.org/pep-0008/): Python baseline preserving project consistency and compatibility.
- [Uber Go](https://github.com/uber-go/guide/blob/master/style.md): Go engineering reference; do not blindly adopt historical tool names.
- [Alibaba Java manual](https://github.com/alibaba/p3c): Chinese rule writing and Java conventions. The repository provides the Huangshan PDF; the old GitBook warns it differs from newer editions.
- [Alibaba frontend conventions](https://github.com/alibaba/f2e-spec), [Airbnb JavaScript](https://github.com/airbnb/javascript): choose one applicable style and check toolchain compatibility.
- [Microsoft C# conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions): primarily examples/documentation, not every .NET project.
- [Microsoft Azure REST API Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/azure/Guidelines.md): consistent interfaces, retries/idempotency, and version compatibility. Do not directly apply Azure-specific conventions.

## Security Attribution and Adaptations

- [Tencent/secguide](https://github.com/Tencent/secguide): source of the code-security guidance. Original attribution: Tencent, THL A29 Limited; license: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This skill reorganizes applicability checks, adds verification criteria, and limits historical examples; see [tencent-security.md](tencent-security.md).
- The original README lists guide revision dates of 2021-05-18. Adopt security objectives, not old-version requirements, simplistic blacklists, or company-specific constants as universal implementations.
- Current [Python subprocess security notes](https://docs.python.org/3/library/subprocess.html#security-considerations) support separating programs and arguments; [pathlib](https://docs.python.org/3/library/pathlib.html) distinguishes lexical paths and symlinks; [hashlib](https://docs.python.org/3/library/hashlib.html) distinguishes digests and password derivation. Check specific APIs against the target runtime.
- Cryptography, authentication, and framework defaults change. If a concrete choice lacks evidence, consult current official sources; otherwise state what remains unconfirmed, not invented security guarantees.

When maintaining this skill, preserve attribution, adaptations, authority boundaries, and risk-based applicability. Do not turn every newly discovered issue into a universal extra process.
