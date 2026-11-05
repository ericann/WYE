# Wye — Salesforce Runtime Analysis Workspace

**中文 | English**

Wye is a runtime analysis workspace for Salesforce Orgs. It brings multi-Org operations into one workspace and is being developed around two core analysis pillars: **Permission** and **Reference**.

Wye helps Salesforce professionals understand how an Org is configured, how access is granted, and how resources relate to one another — providing context for investigation, operational work, and technical decisions.

Wye 是面向 Salesforce Org 的运行时分析工作空间。它将多 Org 管理整合到统一工作环境，并围绕 **Permission（权限分析）** 与 **Reference（资源关系分析）** 两大核心支柱持续演进。

Wye 希望帮助 Salesforce 专业人员理解 Org 的配置、访问权限的授予方式，以及不同资源之间的关系，为问题调查、日常操作和技术决策提供上下文依据。

---

## Product Direction | 产品方向

### Multi-Org Runtime | 多 Org 运行基础

Manage and work across multiple Salesforce Orgs through a unified session and workspace experience. Multi-Org is the runtime foundation that allows analysis and operations to be performed in the correct Org context.

通过统一的 Session 与工作空间管理多个 Salesforce Org。Multi-Org 是 Wye 的运行基础，确保分析与操作能够在正确的 Org 上下文中执行。

### Permission Analysis | 权限分析

Understand access at the Object, Field, and Record levels. Wye's Permission direction focuses not only on showing permission settings, but also on explaining effective access and the sources behind it.

从 Object、Field 与 Record 层面理解访问权限。Permission 的目标不仅是展示权限配置，还包括解释最终有效访问状态及其授权来源。

### Reference Analysis | 资源关系分析

Explore how Salesforce resources are related. The planned Resource / Relationship model uses Object and Field as natural entry points to discover related metadata such as Buttons, Flows, Apex Classes, and Triggers, with evidence and relationship semantics.

探索 Salesforce 资源之间的关联。Reference 计划通过 Resource / Relationship 模型，以 Object 和 Field 为自然入口，发现 Button、Flow、Apex Class、Trigger 等相关 Metadata，并保留关系语义与证据。

> Permission and Reference are evolving analysis capabilities. Their planned scope and delivery status are tracked in the roadmap; this description should not be read as a claim that every planned capability is already available.
>
> Permission 与 Reference 仍在持续演进。具体规划范围与交付状态以 Roadmap 为准；本介绍不代表所有规划能力均已交付。

---

## Workspace Capabilities | 工作空间能力

Wye brings together Salesforce workflows and utilities, including:

- **Multi-Org management** — organize Org sessions with aliases and groups.  
  **多 Org 管理** — 通过别名与分组组织 Org Session。
- **Org access** — open an existing authenticated Org session without repeatedly entering credentials.  
  **Org 访问** — 使用已有认证 Session 访问对应 Org，减少重复登录操作。
- **Metadata search** — search Salesforce metadata across the workspace and inspect matching component types.  
  **Metadata 搜索** — 在工作空间中搜索 Salesforce Metadata，并查看匹配的组件类型。
- **Record API name inspection** — inspect and copy API names from Salesforce record pages.  
  **Record API Name 查看** — 在 Salesforce 记录页面查看并复制 API Name。
- **Data utilities** — run batch query and data-ingestion workflows.  
  **数据工具** — 执行批量查询与数据导入相关工作流。
- **Developer utilities** — access selected debugging and development operations, such as log and trace-flag management and anonymous Apex execution.  
  **开发辅助工具** — 使用日志与 Trace Flag 管理、Anonymous Apex 执行等开发辅助能力。

The exact availability of individual capabilities may depend on the current release and the connected Org's permissions.

具体功能可用性可能取决于当前发布版本，以及已连接 Org 中用户自身的权限。

---

## Design Principles | 设计原则

- **Context before action** — make the target Org and analysis context explicit.  
  **先明确上下文，再执行操作** — 明确目标 Org 与分析上下文。
- **Analysis over isolated utilities** — organize capabilities around understanding an Org, not merely collecting unrelated tools.  
  **分析优先于工具堆叠** — 围绕理解 Org 组织能力，而不是简单罗列互不相关的工具。
- **Evidence-aware explanations** — distinguish observed results, confirmed relationships, inferred relationships, and unresolved information.  
  **解释应尊重证据** — 区分实际观察结果、已确认关系、推断关系与尚未明确的信息。
- **Progressive capability** — deliver reliable, bounded analysis before expanding toward compound analysis and simulation.  
  **渐进式能力建设** — 先交付可靠且边界清晰的分析，再逐步扩展复合分析与模拟能力。

---

## Roadmap | 产品与工程路线图

See **[ROADMAP.md](./ROADMAP.md)** for the bilingual product and engineering roadmap, including phases, execution priorities, and milestones.

产品与工程路线图（中英双语）请参阅 **[ROADMAP.md](./ROADMAP.md)**，其中包含阶段规划、执行优先级与里程碑。

---

## Project Status | 项目状态

Wye is actively evolving. The roadmap documents the intended direction and separates current foundations from capabilities that are still being designed or implemented.

Wye 仍在持续演进。Roadmap 用于记录产品方向，并明确区分当前基础能力与仍处于设计或开发阶段的能力。

---

## Privacy | 隐私

Wye's privacy practices are described in the project's Privacy Policy. Please review the policy before using the extension.

Wye 的数据与隐私实践请参阅项目的 Privacy Policy。使用扩展前，请阅读相关政策。
