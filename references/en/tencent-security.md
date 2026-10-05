# Tencent-Derived Code Security Baseline

English translation | [Chinese rule source](../zh-CN/tencent-security.md) | Paired revision: `2026-10-05.9`

Security guidance derives from [Tencent/secguide](https://github.com/Tencent/secguide). These are reorganized applicability checks for LLM-assisted development, not Tencent's original wording or a completed security audit. Tencent material is published under CC BY 4.0; this file adds risk routing, verification requirements, and historical-example limitations.

## Usage

Check only current changes and their direct input/output/call boundaries. Identify untrusted inputs, execution/storage/rendering, identity/permissions, and sensitive data, then select applicable requirements. Mark irrelevant items not applicable; tool-call counts do not establish security success.

The source README lists a revision date of 2021-05-18. Historical runtime versions, password policies, or simplistic filtering examples are not general security guarantees today. Check concrete implementations against project versions, trusted libraries, and current official documentation.

## General Security Requirements

| Trigger | Required outcome | Targeted verification |
| --- | --- | --- |
| External input | Validate type, range, length, and structure at trust boundaries; reject invalid inputs. | Null/empty, excessive length, wrong type, boundary values. |
| Identity and permissions | Authenticate on the server; authorize by operation and resource/tenant; deny by default. | Unauthenticated, unauthorized, cross-user/cross-tenant access. |
| Database | Parameterize values; controlled mappings for dynamic identifiers; inspect raw ORM queries too. | Injection cannot alter query structure; legitimate special characters still work. |
| System commands/execution | Prefer library APIs; when necessary use a fixed executable, argument array, controlled options, and resource limits. | Metacharacters, leading options, wrong executable, timeout/cancellation. |
| Files/uploads/archives | Ensure the actual destination is within allowed directories; limit type, size, and resources; do not expose an executable-file entrypoint. | Absolute paths, traversal, same-prefix directories, symlinks, archive entries. |
| External URLs/downloads | Constrain protocol/destination to business needs; consider resolved addresses, redirects, and network boundaries. | Disallowed protocol/address, redirect to forbidden targets, resource limits. |
| Pages/templates | Render safely for the output context; use mature sanitizers for rich text; do not execute untrusted text. | HTML/script/attribute/URL injection. |
| Serialization/XML | Do not reconstruct executable objects from untrusted data; disable dangerous entities and external-resource resolution as needed. | Malicious serialized/entity input is rejected or parsed safely. |
| Secrets/sensitive data | No secrets in source, frontend, or logs; minimize response fields, sanitize server-side, use dedicated secure password storage. | Inspect diffs, logs, errors without exposing real secrets. |
| Communication/cryptography | Do not disable TLS verification to fix connectivity; use maintained cryptographic components and appropriate key management. | Bad certificates/configuration fail rather than silently pass. |
| Resources/concurrency | Bound size, timeouts, concurrency, and lifetimes; errors do not cause leaks or endless retries. | Oversized/truncated input, races, cancellation, repeat calls. |
| Errors/configuration/dependencies | External errors reveal no internals; no production debug backdoors; check new dependency provenance/known risks. | Error responses, production configuration, lockfiles, existing scan results. |

Verify locally with synthetic data and isolated tests. Do not proactively scan the public internet, probe production networks, or use real credentials.

## Language References

- **Python**: [Tencent Python guide](https://github.com/Tencent/secguide/blob/main/Python%E5%AE%89%E5%85%A8%E6%8C%87%E5%8D%97.md). Focus on SQL, subprocesses, paths, external URLs, unsafe YAML/object deserialization, XML, and production debug settings.
- **Java**: [Tencent Java guide](https://github.com/Tencent/secguide/blob/main/Java%E5%AE%89%E5%85%A8%E6%8C%87%E5%8D%97.md). Focus on injection, file/network input, sensitive data, and business-access boundaries; check actual framework behavior.
- **JavaScript / TypeScript / Node.js**: [Tencent JavaScript guide](https://github.com/Tencent/secguide/blob/main/JavaScript%E5%AE%89%E5%85%A8%E6%8C%87%E5%8D%97.md). Focus on DOM/HTML insertion, dynamic execution, URLs, `postMessage` origins, subprocesses, queries, Cookies, and sensitive configuration.
- **Go**: [Tencent Go guide](https://github.com/Tencent/secguide/blob/main/Go%E5%AE%89%E5%85%A8%E6%8C%87%E5%8D%97.md). Focus on external lengths/indices, commands/paths, queries, TLS, shared state, and goroutine termination.
- **C / C++**: [Tencent C/C++ guide](https://github.com/Tencent/secguide/blob/main/C%2CC%2B%2B%E5%AE%89%E5%85%A8%E6%8C%87%E5%8D%97.md). Focus on boundaries, length/integer conversions, memory lifetime, format strings, system interfaces, and sensitive data.
- Other languages use general security objectives and actual official language/framework security APIs. Do not claim Tencent provides a dedicated guide when it does not.

For specific high-risk APIs with insufficient local evidence, read relevant original guidance and current API documentation. Do not load all language manuals for every task.

## Historical Examples Not to Copy Blindly

These limitations are this skill's engineering adaptations, not Tencent's original clauses:

- SQL character-removal blacklists do not replace parameter binding. Data validation and query-structure safety are different checks.
- Shell character replacement does not ensure command safety. Argument arrays still need protection against executable option injection; do not wrap external input in concatenated `sh -c` commands.
- Absence of `..` or matching string prefixes does not prove containment. Use path-component/directory-boundary checks and handle symlinks and check/use races according to the threat model.
- SHA-2 is a digest, not reversible encryption. General fast hashes are not direct password-storage schemes. Do not invent cryptographic algorithms or parameters.
- Old runtimes, component names, and example dependencies are not minimum supported versions; check project support and current maintenance status.
- Log retention, password length, enterprise domains, and filename lengths depend on business/compliance/current policy. Do not hardcode Tencent's business environment.

For existing related unsafe code, explain evidence and repair scope; do not rewrite unrelated modules to satisfy this baseline. Report blockers when current security goals cannot be met, not claims of secure completion.
