---
name: development-standards
description: >-
  Govern software development, defect fixes, refactoring, and interface changes with approved requirements, new-project stack selection, and module design; use lightweight paths for scoped low-risk repairs and behavior-preserving refactors. Apply engineering quality and Tencent-derived security guidance. Explanation, diagnosis, and review alone do not authorize edits. 规范开发、缺陷修复、重构与接口变更：正式开发先确认需求、新项目技术栈和模块架构，低风险局部修复及行为保持重构保持轻量；纯解释、诊断和评审不授权修改。支持中英文。
---

# Development Standards / 开发要求与编码规范

One skill, one workflow, two resource languages. / 一个技能、一套流程、两种资源语言。

Paired resource revision / 双语资源配对修订：`2026-10-05.9`。This identifies the resource bundle, not project approval or passed verification. / 仅标识资源包，不代表项目批准或验证通过。

## Language Selection / 语言选择

- Choose the instruction language from the user's explicit preference; otherwise use `zh-CN` for Chinese requests and `en` for English requests. For other languages use English resources and reply in the user's language. Do not infer language from UI metadata or the language of source files.
  规则语言优先遵循用户明确偏好，否则中文请求选 `zh-CN`、英文请求选 `en`；其他语言使用英文资源并以用户语言沟通。不根据界面配置或源文件语言推断用户偏好。
- For conversation, follow the user's requested language, otherwise their current request. For each document, use its explicitly requested language, otherwise the project's existing documentation convention, otherwise the conversation language. Use the matching template; for other languages adapt an English template. Do not translate unrelated files or rename code identifiers as a side effect.
  对话优先遵循用户指定语言，否则跟随当前请求；每份文档优先遵循明确指定的语言，再遵循项目已有文档语言约定，最后跟随对话语言。使用相应模板，其他语言可基于英文模板调整；不顺带翻译无关文件或重命名代码标识符。
- Before task work, read exactly one corresponding baseline below, then only its references relevant to the task. A requested document language can differ from the instruction language; do not load both complete resource sets just for that reason.
  开始任务工作前读取下方一种语言的核心规范，再按需加载其中相关参考。文档目标语言可与规则语言不同，不因此加载两套完整资源。

| Baseline / 核心规范 | When to read / 读取条件 |
| --- | --- |
| [中文规范](references/zh-CN/standards.md) | Chinese instruction language / 规则语言为中文 |
| [English Standards](references/en/standards.md) | English or fallback instruction language / 规则语言为英文或使用英文回退 |

## Shared Invariants / 共同约束

- For formal development, approve requirements first, then the complete module/architecture design for the current implementation scope; new projects also require explicit stack confirmation. Partial approval covers only identified scope; necessary dependencies must also be approved, not implicitly included. Do not implement or scaffold before applicable gates pass. Reuse authentic, applicable approvals; never fabricate them.
  正式开发先确认需求，再确认本次实施范围的完整模块架构；新项目还须明确确认技术栈。部分确认仅覆盖指定范围，必要依赖也须已确认，不自动扩大批准。适用门槛未通过前不实施或初始化工程；复用真实有效确认，不伪造批准。
- During architecture design, complex modules require architecture diagrams and complex workflows require flowcharts, saved with the design and consistent with module/interface descriptions. Missing required diagrams leave that scope incomplete; diagrams do not replace contracts or add an approval stage. Simple designs and read-only/lightweight tasks do not require whole-project diagram backfill.
  架构设计阶段，复杂模块必须用架构图、复杂流程必须用流程图表示，随设计文档保存并与模块/接口说明一致。缺少必需图示时对应范围设计不完整；图不替代契约、不新增审批。简单设计及只读/轻量任务不要求补画全项目图。
- When interface design is needed, deliver three genuinely distinct browser-viewable HTML visual prototypes for the same scoped requirements and representative screens, prioritizing aesthetics, layout, typography, and visual hierarchy. Static HTML/CSS is sufficient; JavaScript and interaction demos are optional unless explicitly requested. Provide entries and actual rendering-check results, record trade-offs and the user's selection before formal implementation. Isolated design work does not bypass requirements/stack/architecture gates or authorize live services. Reuse valid applicable selections; read-only reviews and repairs preserving established design do not force reselection.
  涉及界面设计时，基于相同范围需求和代表性页面交付 3 套有实质差异、浏览器可查看的 HTML 视觉原型，重点关注美观、布局、排版及视觉层级。静态 HTML/CSS 示意页面即可，JS 与轻量交互默认可选；用户明确要求交互演示时按指定范围实现。提供入口及真实渲染检查结果，记录取舍和用户选择后再正式实施。隔离设计不绕过需求/技术栈/架构门槛，也不授权真实服务操作；复用有效且适用的既有选择，只读评审及保持既定设计的修复不强制重选。
- At the start of coding, check whether the scoped implementation uses a database. If so, output and save its design before database-related code: propose a new database or inspect and reuse/update existing design, defaulting to `docs/database-design.md`. No database means no database document. This is a coding deliverable, not an architecture-approval prerequisite or extra approval stage. Applicable scope-change and data-operation safeguards still apply; read-only work does not authorize edits.
  开始编码时检查本次实现是否使用数据库；涉及时，数据库相关代码前必须输出并保存设计，默认 `docs/database-design.md`：新库给出方案，已有库先核对并复用/更新现有设计。不使用数据库则不生成该文档。它是编码阶段交付物，不是架构批准的前置附件，不增加审批阶段；仍遵守范围变更和数据操作安全要求，只读工作不授权编辑。
- Every complete project-code change, including bug fixes and refactors, must increment the affected product version under its established scheme. Update the actual version source and required synchronized entries before handoff, reporting old/new values and locations. Count one complete change, not each file edit or retry. Pure documentation/read-only work does not trigger a product bump; unclear schemes or authority conflicts require clarification. Version bumps do not authorize release or waive compatibility.
  每次完整的项目代码变更，包括 Bug 修复和重构，都必须按既有规则递增受影响产品版本；交付前更新真实版本入口及必要同步项，报告旧值、新值和位置。按完整变更计数，不按文件编辑或重试次数；纯文档/只读工作不触发产品升版，规则不明或授权冲突时先澄清。升版不授权发布，也不豁免兼容要求。
- Qualifying low-risk localized repairs restore clear intent; qualifying behavior-preserving refactors retain observable behavior, errors, and side effects. Both stay within authorized scope without new features, contract/boundary changes, or high-risk effects. State the goal, evidence, scope, and verification plan; do not force historical product-document backfill or redundant approval. Clarify ambiguity and escalate affected work when scope or risk increases.
  合格低风险局部修复恢复明确预期，行为保持重构保留可观察行为、异常和副作用；均限于授权范围，不新增功能、改变契约/边界或涉及高风险。简述目标、依据、范围和验证方式，不追补历史产品文档或重复审批；有歧义先澄清，范围或风险扩大时升级受影响流程。
- For client/Server products, Server changes must preserve older product Agents' protocols, interfaces, field semantics, and core workflows without forced Agent upgrades. User/project compatibility scope and actual older-Agent evidence are required for affected interactions. Incompatibility, failed or missing verification blocks merge/release, not just a warning. Agent here is a software client, not an LLM.
  对客户端/Server 产品，服务端改动须保持低版本产品 Agent 的协议、接口、字段语义及核心流程，不强制升级 Agent。涉及交互时遵循用户/项目兼容范围并提供实际低版本证据；不兼容、验证失败或缺失阻断合并发布。Agent 指软件客户端，不是大模型。
- Preserve user scope, repository rules, and higher-priority instructions. Read-only requests do not authorize edits. Approval does not grant unrelated commit, push, PR, deployment, production-data, or external-write permissions. Report actual evidence and unverified work; self-review is not independent review.
  遵守用户范围、仓库规则及更高优先级指令；只读请求不授权编辑，批准不授予无关提交、推送、PR、部署、生产数据或外部写入权限。按实际证据报告未验证项，自审不冒充独立审查。

## Translation Maintenance / 翻译维护

| Term / 术语 | Meaning / 含义 |
| --- | --- |
| Required / 必须 | Applicable obligation, not a suggestion / 适用时须满足，不是建议 |
| Must not / 不得 | Prohibited action / 禁止的操作 |
| Recommended / 建议 | Preferred, with justified adaptation allowed / 优先采用，可按依据调整 |
| Approved / 已确认 | Authentic approval of identified content and scope / 真实确认指定内容与范围 |
| Verified / 已验证 | Relevant checks actually passed, not approval or deployment / 相关检查实际通过，不等于批准或部署 |

`references/zh-CN` and `assets/zh-CN` are the Chinese rule/template sources; the matching `en` files are translations, not independent policies. Update corresponding files, links, READMEs, and affected behavioral scenarios together; advance the bundle's paired revision in this entrypoint, both READMEs, and resource headers. A matching revision is not proof of semantic equivalence. Keep the terms above, task modes, safety constraints, and evidence standards equivalent. Language switching alone does not invalidate approvals or authorize work. If a discrepancy is discovered, report it and consult only the affected Chinese source; do not silently select a weaker translation. If the source cannot be checked, disclose the uncertainty and do not claim the affected gate passed. Higher-priority instructions remain controlling.

`references/zh-CN` 和 `assets/zh-CN` 是中文规则/模板源，同名 `en` 文件是译文，不是独立政策。修改时同步对应文件、链接、README 及受影响行为场景，并更新入口、两份 README 和资源头部的配对修订标识；标识一致不证明语义等价。保持上表术语、任务模式、安全约束和证据标准等价。仅切换语言不使批准失效或授予实施权限。发现差异时报告并仅核对受影响中文源，不静默选择更宽松译文；源文无法核验时说明不确定性，不声称相关门槛已通过。更高优先级指令始终优先。
