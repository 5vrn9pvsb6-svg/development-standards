# 来源与适用限制

中文规则源 | [English](../en/sources.md) | 配对修订：`2026-10-05.9`

整理核对日期：2026-10-03。链接为官方公开来源，指向会变化的页面，未承诺固定版本。本 Skill 是原创的操作性整理，不是手册全文复制、官方认证或任何公司的内部制度。

正式开发的需求与本次实施范围的完整架构必须分别讨论、落盘并经用户确认后才编码，是本 Skill 用户指定的开发门槛。预期明确、范围可核验的低风险局部修复及行为保持重构采用轻量通道、不追补历史产品文档，也是用户选择的流程规则；文档模板、需求到模块的映射及维护记录方式是配套整理，不宣称为某家公司的原文或统一制度。

新项目正式开发前与用户确认技术栈，并为非技术用户提供易懂的可行方案，也是用户指定的流程要求；选型比较、记录方式和换栈确认是配套整理，不归因于某家公司的公开制度。

低版本客户端 Agent 兼容性红线也是用户指定的产品约束，不归因于腾讯安全指南或其他公司的公开制度；协议兼容设计和验证证据要求是该约束的配套整理。

单入口双语结构、语言选择、中文规则源及成对翻译维护也是用户选择的技能约定，不归因于某家公司的工程制度。

开始编码时检查是否使用数据库，涉及时输出并独立保存当前范围的数据库设计；新库提出设计，已有库核对并复用/更新文档，不使用数据库则跳过，也是用户指定的要求。数据库文档放在编码阶段，不作为架构审批的前置附件，不增加独立审批；模板、文档/实现一致性、范围变更与只读边界是配套整理，不归因于某家公司的公开制度。

架构设计阶段，复杂模块必须用架构图、复杂流程必须用流程图表示，也是用户指定的要求；复杂度判断、落盘/一致性检查及简单/轻量/只读边界是配套整理，不宣称为某家公司的统一画图制度，不另加审批阶段。

每次修改项目代码（包括 Bug 修复）递增产品版本，也是用户指定的要求，不宣称为某家公司的统一规定。按完整变更计数、真实版本入口与必要同步、续接不重复升版及只读/发布授权边界是配套整理；产品版本不同于本 Skill 配对修订或项目文档内容版本。

涉及界面设计时输出 3 套浏览器可查看的 HTML 视觉原型，重点关注美观及视觉效果，也是用户指定并修订的要求，不归因于某家公司的统一制度。静态 HTML/CSS 示意页面即可，JS/交互默认可选，明确要求时才按范围演示，以减少方案阶段成本。实际渲染检查、同范围比较、设计记录/真实选择、复用既有确认及只读/原型边界是配套整理；单独图片/文字不能替代 HTML 入口，视觉原型不等于功能完成，不授权提前实施产品代码或连接真实业务服务，也不新增固定审批台账。

模块及手写源文件职责清晰，并在没有项目长度约定时以 1000 行作为拆分评估阈值，是用户选择的编码约束，不是大厂统一上限。物理行计数、按职责拆分、保留理由、生成/锁文件/第三方代码例外及任务范围边界是配套整理；超过阈值必须评估，不代表一律禁止或授权无关重构。

## 工程流程与质量

- [Microsoft ISE Engineering Fundamentals Playbook](https://microsoft.github.io/code-with-engineering-playbook/)：流程骨架。其 [Ready](https://microsoft.github.io/code-with-engineering-playbook/agile-development/team-agreements/definition-of-ready/)、[Done](https://microsoft.github.io/code-with-engineering-playbook/agile-development/team-agreements/definition-of-done/)、[设计模板](https://microsoft.github.io/code-with-engineering-playbook/design/design-reviews/recipes/templates/feature-story-design-review/) 和 [工程清单](https://microsoft.github.io/code-with-engineering-playbook/engineering-fundamentals-checklist/) 用于需求/设计/完成条件；示例覆盖率、审批人数和组织角色不自动采用。
- [Google Engineering Practices](https://google.github.io/eng-practices/review/reviewer/looking-for.html)、[Small CLs](https://google.github.io/eng-practices/review/developer/small-cls.html)：自审维度和聚焦改动。
- [Software Engineering at Google](https://abseil.io/resources/swe-book/html/toc.html)：长期维护背景；[规则制定](https://abseil.io/resources/swe-book/html/ch08.html) 与 [单元测试](https://abseil.io/resources/swe-book/html/ch12.html) 为阅读者优先和有效测试提供参考。
- [GitLab 开发工作流](https://docs.gitlab.com/development/contributing/merge_request_workflow/)：提交、验收和上线后责任参考；其产品专用验收要求不作为通用规则。
- [AWS 自动测试与回滚](https://docs.aws.amazon.com/wellarchitected/latest/framework/ops_mit_deploy_risks_auto_testing_and_rollback.html)：生产交付的成功/失败信号及恢复要求，不要求接入 AWS。

## 编码约定

- [Google Style Guides](https://google.github.io/styleguide/)；[Python](https://google.github.io/styleguide/pyguide.html)、[Go](https://google.github.io/styleguide/go/)、[Java](https://google.github.io/styleguide/javaguide.html)、[C++](https://google.github.io/styleguide/cppguide.html)。以对应项目约定为准。
- [PEP 8](https://peps.python.org/pep-0008/)：Python 基础约定，明确保留项目一致性和兼容性。
- [Uber Go](https://github.com/uber-go/guide/blob/master/style.md)：Go 工程编码参考，不盲用历史工具名称。
- [阿里 Java 手册](https://github.com/alibaba/p3c)：中文条款写法和 Java 规约参考；仓库提供黄山版 PDF，旧 GitBook 已提示与新版不同。
- [阿里前端规约](https://github.com/alibaba/f2e-spec)、[Airbnb JavaScript](https://github.com/airbnb/javascript)：按项目选一套，核对工具链兼容性。
- [微软 C# 约定](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)：该页面主要面向示例/文档，不等同于所有 .NET 项目。
- [Microsoft Azure REST API Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/azure/Guidelines.md)：接口一致性、重试/幂等和版本兼容；Azure 专用约定不直接套用。

## 安全来源与工程修订

- [Tencent/secguide](https://github.com/Tencent/secguide)：本 Skill 的代码安全指南来源。原资料署名为腾讯公司 THL A29 Limited，许可 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)。本 Skill 重新组织为适用性检查、增加验证条件，并对历史样例提出限制，详见 [tencent-security.md](tencent-security.md)。
- 原 README 显示各指南修订日期为 2021-05-18。采用安全目标，不把旧版本要求、简单黑名单或企业业务常量直接变成通用实现。
- 当前 [Python subprocess 安全说明](https://docs.python.org/3/library/subprocess.html#security-considerations) 支持优先分离程序和参数；[pathlib](https://docs.python.org/3/library/pathlib.html) 说明词法路径检查与符号链接处理的区别；[hashlib](https://docs.python.org/3/library/hashlib.html) 明确区分摘要与密码派生。具体 API 必须核对目标运行版本。
- 密码学、认证和框架默认值可能变化。涉及具体选择且证据不足时查当前官方资料；无法核对时说明未确认项，不臆造安全保证。

更新本 Skill 时保留来源、修订说明、授权边界和按风险启用的机制；不要把新发现的单一问题扩展为所有任务的普遍额外流程。
