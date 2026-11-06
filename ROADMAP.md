# Wye 产品路线图 | Product Roadmap

> Wye is a runtime analysis workspace for Salesforce Orgs. Multi-Org provides the runtime foundation; Permission and Reference are the two core analysis pillars.
>
> Wye 是面向 Salesforce Org 的运行时分析工作空间。Multi-Org 提供运行基础，Permission 与 Reference 是两大核心分析支柱。

本路线图面向用户与潜在用户，描述产品方向和阶段性目标。它不承诺具体发布日期，也不代表所有规划能力已经交付。工程任务、技术设计与内部优先级由私有研发仓库管理。

This roadmap is intended for users and prospective users. It describes product direction and staged outcomes, not guaranteed release dates or claims that planned capabilities are already available. Engineering tasks, technical designs, and internal priorities remain in the private development repository.

---

## 产品方向 | Product Direction

Wye 希望帮助 Salesforce 专业人员理解 Org 的访问控制、Metadata 关系及运行上下文，为问题调查、日常操作和技术决策准备可靠的信息与证据。

Wye helps Salesforce professionals understand access control, metadata relationships, and runtime context within an Org, preparing reliable information and evidence for investigation, operations, and technical decisions.

## 产品基础 | Workspace Foundation

- **Multi-Org workspace** — organize multiple Org sessions and keep operations in the correct Org context.
- **Contextual operations** — access an authenticated Org session and run supported Salesforce operations without repeatedly switching tools.
- **Metadata discovery** — search metadata across connected Orgs and inspect matching component types.
- **Developer utilities** — provide selected query, data, debugging, and development workflows.

## 核心分析能力 | Core Analysis

### Permission Analysis

逐步从权限配置展示，推进到有效访问结果与授权来源解释，覆盖 Object、Field，并在明确边界内扩展 Record Access。

Move from displaying permission configuration toward explaining effective access and its grant sources across Object, Field, and, within clearly defined boundaries, Record Access.

### Reference Analysis

以 Object 与 Field 为自然入口，探索 Salesforce Metadata 资源之间的关系，并为关系提供可追溯的证据与语义。

Use Object and Field as natural entry points to explore relationships among Salesforce metadata resources, with traceable evidence and explicit relationship semantics.

---

## 阶段规划 | Staged Direction

| 阶段 | 目标 |
|---|---|
| Runtime Foundation | Improve multi-Org context consistency, session reliability, and operational safety. |
| Permission Analysis | Deliver trustworthy Object and Field access explanations, then expand supported Record Access attribution. |
| Reference Analysis | Establish an evidence-backed Resource / Relationship model and useful metadata exploration. |
| Advanced Analysis | Add meaningful comparison, impact analysis, and carefully scoped what-if evaluation. |
| Unified Org Analysis | Connect permission and resource context to support compound investigation and cross-Org understanding. |

阶段之间可能根据验证结果调整。优先级以可靠性、可验证性和实际调查价值为依据，而不是单纯增加功能数量。

The sequence may change as capabilities are validated. Priorities are guided by reliability, verifiability, and practical investigation value rather than feature count alone.

## 状态说明 | Status

- Roadmap items describe intended direction, not guaranteed delivery dates.
- A capability is considered delivered only after implementation, integration, and validation.
- Supported behavior may depend on the Wye release and the connected Salesforce Org's permissions.
- Public feedback is welcome through [GitHub Issues](https://github.com/ericann/WYE/issues).

## 反馈与参与 | Feedback

发现问题、希望支持新的分析场景，或对产品方向有建议？欢迎通过 [WYE Issues](https://github.com/ericann/WYE/issues) 提交。请勿在公开 Issue 中提交 Salesforce Session、Token、客户数据或其他敏感信息。

Have a bug report, a use case, or feedback on product direction? Please use [WYE Issues](https://github.com/ericann/WYE/issues). Never include Salesforce sessions, tokens, customer data, or other sensitive information in public issues.
