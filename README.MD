# Skill Engine

本仓库用于沉淀和维护 Codex 可用的本地 Skills。当前包含两个面向软件工程协作的技能：

- `requirements-task-planner`：需求澄清、需求冻结与任务规划。
- `code-review-governance`：架构视角代码审查、工程治理与风险分级。

这些 Skills 不是业务项目代码，而是给 Codex/Agent 使用的工作流说明、输出规范和辅助模板。目标是让需求分析、任务拆解、代码审查和工程治理过程更稳定、更可复用。

## 目录结构

```text
skill-engine/
├── README.MD
├── requirements-task-planner/
│   ├── SKILL.md
│   └── agents/
│       └── openai.yaml
└── code-review-governance/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── prompts/
        ├── architecture-review-template.md
        ├── engineering-governance-template.md
        ├── non-functional-checklist.md
        ├── output-template.md
        ├── pr-description-template.md
        ├── quick-review-template.md
        ├── review-checklists.md
        ├── review-workflow.md
        ├── risk-assessment-template.md
        ├── security-checklist.md
        └── testing-verification-checklist.md
```

## Skills 概览

### requirements-task-planner

用于在开始编码前完成需求分析和任务规划。它强调先收集、验证并冻结需求，再输出任务规划文档，最后才进入实现阶段。

适用场景：

- 用户需求不完整、存在歧义或边界不清。
- 需要输出需求分析、实施计划、任务拆解、里程碑或验收标准。
- 需要在 Quick、Standard、Deep Analysis 三种模式之间选择合适规划深度。
- 需要用 Mermaid 表达流程、状态、模块关系、类关系或系统交互。

核心规则：

- 需求不完整时先提问，不直接规划。
- Standard 和 Deep Analysis 模式需要经过需求冻结确认。
- 冻结后主动生成 Markdown 任务规划文档。
- 规划文档完成前不开始修改源代码。

默认提示：

```text
Use $requirements-task-planner to clarify requirements and produce an appropriately scoped task plan.
```

### code-review-governance

用于从技术负责人、架构师和工程治理视角做代码审查。它不只关注语法、lint 或局部 bug，而是重点检查需求/设计一致性、架构边界、模块职责、可维护性、测试证据、安全和非功能风险。

适用场景：

- 审查 PR、变更集或整个仓库的工程质量。
- 评估实现是否符合需求文档、设计文档、任务计划或架构约定。
- 检查前端、Java/Spring、多模块、微服务或全栈项目的模块边界和长期维护风险。
- 给出合并/发布结论、风险等级、豁免要求和技术债跟踪建议。

核心规则：

- 先确认审查范围、准入证据和验证状态。
- 先审查需求/设计一致性，再审查架构和实现细节。
- 风险等级使用 `致命 / 高风险 / 中风险 / 建议优化`。
- 合并/发布结论统一遵循 `prompts/risk-assessment-template.md`。
- 默认先输出审查摘要，不自动生成大型后续文档，除非用户要求。

默认提示：

```text
Use $code-review-governance to review this repository for architecture consistency, maintainability, and engineering governance risks.
```

## 安装方式

将需要使用的 Skill 目录复制到 Codex 的本地 skills 目录即可。常见路径如下：

```text
C:\Users\<用户名>\.codex\skills\
```

示例：

```powershell
Copy-Item -Recurse .\requirements-task-planner C:\Users\<用户名>\.codex\skills\
Copy-Item -Recurse .\code-review-governance C:\Users\<用户名>\.codex\skills\
```

复制后重启 Codex 会话或刷新运行环境，使新的 Skill 被重新发现。

## 使用示例

### 需求规划

```text
使用 $requirements-task-planner，帮我梳理一个订单审批功能的需求，并输出任务规划。
```

当需求不完整时，Skill 会先提出澄清问题；当需求满足冻结条件后，再生成任务规划文档。

### 代码审查

```text
使用 $code-review-governance，审查这个仓库的架构一致性、可维护性和工程治理风险。
```

对于普通 PR，输出会偏向快速审查结论；对于仓库级或架构较重的审查，会结合 `prompts/` 下的模板输出更完整的治理报告。

## 维护约定

- 每个 Skill 必须包含 `SKILL.md`，并在 front matter 中声明 `name` 和 `description`。
- `agents/openai.yaml` 用于配置界面展示名称、简短说明和默认提示。
- 大型模板、清单和参考资料应放在 Skill 内部的 `prompts/` 目录中，避免让 `SKILL.md` 过度膨胀。
- 修改风险等级、合并规则或审查准出标准时，应优先维护单一权威文档，避免多处规则相互冲突。
- 文档语言默认使用中文；如果 Skill 面向英文用户，可以在对应目录内补充英文模板。

## 贡献建议

新增或调整 Skill 时建议按以下顺序检查：

1. Skill 的触发场景是否清晰。
2. 是否有明确的执行边界和停止条件。
3. 是否说明了输入、输出、阶段和质量标准。
4. 是否避免把可复用模板直接堆进主 `SKILL.md`。
5. 是否提供了足够短、可直接使用的默认提示。

## 当前状态

本仓库仍处于技能库迭代阶段，当前重点是沉淀需求规划与代码审查治理流程。后续可以继续扩展：

- 技术设计评审 Skill。
- Java/Spring 专项审查 Skill。
- 前端架构审查 Skill。
- 安全审查或测试策略专项 Skill。
- 团队研发流程与工程治理模板。
