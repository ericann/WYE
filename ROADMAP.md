# Wye 产品与工程路线图 | Product & Engineering Roadmap

> **产品定位 | Product Direction**
>
> **中文：** Wye 是面向 Salesforce Org 的运行时分析工作空间。Multi-Org 是其运行基础，Permission 与 Reference 是两大核心分析支柱。Wye 帮助用户理解 Org 内部的访问控制结构、资源关系及运行逻辑，从而调查问题，并为后续操作与技术决策提供依据。
>
> **English:** Wye is a runtime analysis workspace for Salesforce Orgs. Multi-Org provides its runtime foundation, while Permission and Reference form its two core analysis pillars. Wye helps users understand access-control structures, resource relationships, and Org behavior so they can investigate issues and prepare for operational and technical decisions.

本文档区分当前实现、工程改进任务与未来产品方向。规划中的能力只有在完成集成和验证后，才能视为已交付能力。

This roadmap distinguishes current implementation, engineering improvements, and future product direction. Planned capabilities are not considered delivered until they have been implemented, integrated, and validated.

---

## 路线图概览 | Roadmap at a Glance

| 阶段 Phase | 重点 Focus | 目标 Outcome |
|---|---|---|
| 1 | 运行时可靠性 Runtime Reliability | 确保 Org 上下文、Session、HTTP 请求与缓存行为一致 / Consistent Org context, Session, HTTP, and cache behavior |
| 2 | 工程基础 Engineering Foundation | 建立可重复的测试与构建质量门禁 / Repeatable tests and build quality gates |
| 3 | Permission Analysis V1 | 提供可信的 Object、Field 与限定范围的 Record Access 归因 / Trustworthy Object, Field, and scoped Record Access attribution |
| 4 | 高级权限分析 Advanced Permission Analysis | 实现有实际重算能力的 Compare、What-if 与影响分析 / Meaningful Compare, What-if, and impact recalculation |
| 5 | Reference V1 | 从 Object 与 Field 入口建立 Resource / Relationship 分析 / Resource and Relationship analysis from Object and Field entry points |
| 6 | 统一 Org 分析 Unified Org Analysis | 结合 Permission 与 Reference，支持跨领域及跨 Org 分析 / Combine Permission and Reference for cross-domain and cross-Org analysis |

---

## Phase 1 — 运行时可靠性 | Runtime Reliability

**目标 | Goal**

确保每项操作始终绑定到预期的 Salesforce Org，包括异步任务与并发执行场景。

Ensure every operation remains bound to the intended Salesforce Org, including asynchronous and concurrent work.

### Org 上下文完整性 | Org Context Integrity

- [ ] [#1 — 修复 RestService 强制刷新时目标 Org Host 丢失](https://github.com/ericann/WYE/issues/1)  
  Preserve the target Org Host during RestService forced refresh.
- [ ] [#2 — 为完整分析任务固定 Org 上下文](https://github.com/ericann/WYE/issues/2)  
  Pin the Org context for the full lifetime of an analysis task.

### Session 与缓存完整性 | Session and Cache Integrity

- [ ] [#3 — 修复 ChromeStorageAPI remove / clear 的缓存失效语义](https://github.com/ericann/WYE/issues/3)  
  Correct cache invalidation semantics for ChromeStorageAPI remove / clear.
- [ ] [#4 — Org 切换时等待 Session 注册完成](https://github.com/ericann/WYE/issues/4)  
  Await Session registration during Org switching.

### 浏览器运行时边界 | Browser Runtime Boundaries

- [ ] [#5 — 防止 DOMInspector 重复注册消息监听器](https://github.com/ericann/WYE/issues/5)  
  Prevent duplicate DOMInspector message-listener registration.
- [ ] [#6 — 校验 Background 消息发送者并收紧 Salesforce Cookie 查询范围](https://github.com/ericann/WYE/issues/6)  
  Validate Background message senders and narrow Salesforce Cookie lookup scope.

**完成标准 | Exit Criteria**

- Org A 中启动的任务，即使用户切换当前 Org，也只向 Org A 发出请求。  
  A task started in Org A continues to issue requests only to Org A, even if the selected Org changes.
- 响应数据写入其实际来源 Org 对应的缓存空间。  
  Responses are stored under the cache namespace of the Org from which they were fetched.
- 快速切换 Org 时，Session 状态与 Token 状态保持一致。  
  Session and Token state remain consistent during rapid Org switching.
- 删除缓存后，不会再读取到过期的内存缓存值。  
  Cache deletion cannot return stale in-memory values.
- DOM 变化或导航过程中不会累积重复监听器。  
  Runtime listeners do not accumulate during DOM changes or navigation.
- 消息来源与 Cookie 查询范围有明确校验。  
  Message sources and Cookie lookup scope are explicitly validated.

---

## Phase 2 — 工程基础 | Engineering Foundation

**目标 | Goal**

在扩展分析能力之前，让关键行为具备可重复验证的工程基础。

Establish a repeatable engineering foundation for critical behavior before expanding analysis complexity.

- [ ] [#9 — 建立核心服务自动化测试与构建质量门禁](https://github.com/ericann/WYE/issues/9)  
  Add core automated tests and build quality gates.

**首批测试优先级 | Initial Test Priorities**

1. Multi-Org Session 注册、切换与 Token Refresh。  
   Multi-Org Session registration, switching, and Token refresh.
2. HttpQueueService 的 Org 隔离与并发刷新行为。  
   Org isolation and concurrent refresh behavior in HttpQueueService.
3. ChromeStorageAPI 的 Key、remove、clear 与缓存失效。  
   Key generation, remove, clear, and cache invalidation in ChromeStorageAPI.
4. Permission Set / Permission Set Group 的 Grant 与 Muting 聚合。  
   Grant and Muting aggregation for Permission Sets and Permission Set Groups.
5. RestService 及分析调用链中的显式 Host 传递。  
   Explicit Host propagation through RestService and analysis call chains.

**构建流水线目标 | Target Build Pipeline**

`install → typecheck → tests → build`

优先覆盖高风险路径，不必在初期建立过度复杂的测试框架。

Start with high-risk paths; avoid building an unnecessarily large testing framework at the outset.

**完成标准 | Exit Criteria**

- 在干净环境中可以安装测试依赖并执行测试命令。  
  Test dependencies install and test commands run in a clean environment.
- 核心服务路径具备自动化回归测试。  
  Critical service paths have automated regression coverage.
- TypeScript 类型检查成为构建门禁。  
  TypeScript type checking is enforced as a build gate.
- CI 至少执行 install、typecheck、tests 与 build。  
  CI runs install, typecheck, tests, and build at minimum.

---

## Phase 3 — 权限分析 V1 | Permission Analysis V1

**目标 | Goal**

从权限数据采集与展示，推进到可信的访问结果解释与授权来源归因。

Move beyond permission data collection and presentation toward trustworthy access explanation and grant-source attribution.

### Object 与 Field 权限 | Object and Field Permissions

- 验证 Permission Set / Permission Set Group 的 Grant 与 Muting 组合语义。  
  Validate combined Grant and Muting semantics across Permission Sets and Permission Set Groups.
- 将 Graph 分析接入实际 Permission 分析流程；若暂不接入，则应明确其未集成状态。  
  Integrate Graph analysis into the actual Permission analysis path, or explicitly retain it as unintegrated functionality.
- 确保有效路径分析正确体现 Muting 语义。  
  Ensure effective-path analysis reflects Muting semantics correctly.
- Tree 负责可读的结构与归因；Graph 负责跨分支、复合关系分析。  
  Use Tree for readable structure and attribution; use Graph for cross-branch and compound relationship analysis.
- 增加真实 Org 验证案例与自动化回归测试。  
  Add real-Org validation scenarios and automated regression tests.

相关 Issue | Related Issue: [#7 — 将 Permission Graph 接入主分析流程并正确处理 Muting 路径](https://github.com/ericann/WYE/issues/7)

### Record Access | 记录访问权限

- 区分实际访问结果（例如 UserRecordAccess）与已识别的授权来源。  
  Distinguish actual access outcomes (for example, UserRecordAccess) from identified grant sources.
- 改进直接 User Share 的归因。  
  Improve direct User Share attribution.
- 评估 GroupMember 与嵌套 Group 的展开能力。  
  Evaluate GroupMember and nested Group expansion.
- 明确 Role Hierarchy 与 Sharing Rules 的支持边界。  
  Define support boundaries for Role Hierarchy and Sharing Rules.
- 对部分解析、未知来源或查询失败进行明确标记，不得暗示归因完整。  
  Explicitly mark partial resolution, unknown sources, or query failures instead of implying complete attribution.

相关 Issue | Related Issue: [#8 — 补全 Record Access 的共享来源归因边界](https://github.com/ericann/WYE/issues/8)

**完成标准 | Exit Criteria**

- 已支持的 Object / Field 结果经过真实 Org 行为验证。  
  Supported Object / Field results are validated against real Org behavior.
- Muting 路径不会被错误展示为有效授权。  
  Muting paths are not incorrectly presented as effective grants.
- Record Access 输出清楚区分实际访问状态与已识别的归因来源。  
  Record Access output clearly separates observed access state from identified attribution sources.
- 不支持或无法解析的来源会被明确标记。  
  Unsupported or unresolved sources are explicitly identified.
- Tree 与 Graph 提供不同但相互关联的分析价值。  
  Tree and Graph provide distinct but connected analytical value.

---

## Phase 4 — 高级权限分析 | Advanced Permission Analysis

**目标 | Goal**

使 Permission 能力从当前状态解释，扩展到状态比较与受控模拟。

Extend Permission from explaining the current state to comparing states and performing controlled simulations.

### Compare | 对比分析

支持比较用户、权限分配、Permission Set Group、Org 配置或已捕获状态。分析结果应解释有效权限与访问路径的变化，而不只是原始 Metadata 差异。

Compare users, permission assignments, Permission Set Groups, Org configurations, or captured states. Results should explain changes in effective permissions and access paths, not merely raw metadata differences.

### What-if | 假设模拟

What-if 必须修改分析模型并重新计算影响。仅隐藏节点或比较路径，不构成完整模拟。

A What-if operation must modify an analysis model and recalculate its consequences. Hiding a node or comparing paths alone is not a complete simulation.

建议按以下顺序推进 | Suggested progression:

1. 权限来源变更。  
   Permission-source changes.
2. 重新计算有效授权路径，并纳入 Muting 语义。  
   Recalculate effective grant paths, including Muting semantics.
3. 重新评估 Object、Field 及已支持范围内的 Record Access。  
   Re-evaluate Object, Field, and supported Record Access.
4. 明确区分模拟结果与 Org 当前真实状态。  
   Clearly distinguish simulated results from the actual Org state.

### Impact Analysis | 影响分析

当权限提供方或关系发生变化时，识别哪些权限与访问结果会受到影响。必须区分 Graph 可达性与重新计算后是否仍存在有效授权路径。

Identify which permissions and access outcomes change when a provider or relationship changes. Distinguish graph reachability from whether valid authorization paths remain after recalculation.

**完成标准 | Exit Criteria**

- Compare 具有明确的基准模型与对比模型。  
  Compare has explicit baseline and comparison models.
- What-if 执行实际重算，而不只是改变展示。  
  What-if performs actual recalculation rather than presentation-only changes.
- Impact 结果能够指出受影响的访问结果并解释证据。  
  Impact results identify affected access outcomes and explain their evidence.
- 模拟结果不会被误认为已修改线上 Org。  
  Simulated results are never presented as changes to the live Org.

---

## Phase 5 — Reference V1 | Reference V1

**目标 | Goal**

建立最小化、以证据为基础的 Resource 与 Relationship 模型。

Establish a minimal, evidence-backed Resource and Relationship model.

- [ ] [#10 — 定义并实现 Reference V1：Resource 与 Relationship 模型](https://github.com/ericann/WYE/issues/10)

### 初始范围 | Initial Scope

- 以 Object 与 Field 作为主要分析入口。  
  Use Object and Field as the primary analysis entry points.
- 发现相关的 Button、Flow、Apex Class、Trigger 及其他选定 Metadata 资源。  
  Discover related Buttons, Flows, Apex Classes, Triggers, and selected metadata resources.
- 定义关系语义，避免将所有关联都表达成没有区别的普通边。  
  Define relationship semantics rather than representing every association as an undifferentiated edge.
- 保留关系证据，并区分已确认、推断与可能存在的关系。  
  Preserve relationship evidence and distinguish confirmed, inferred, and possible relationships.
- 从可靠识别的静态或配置关系开始，不承诺完整 Runtime Trace。  
  Start with reliably discoverable static or configuration relationships; do not claim complete runtime tracing.

### 建议模型概念 | Suggested Model Concepts

- **Resource：** 身份、类型、API Name、Org 上下文及相关 Metadata。  
  **Resource:** identity, type, API name, Org context, and relevant metadata.
- **Relationship：** 来源、目标、语义类型、证据及置信度 / 来源信息。  
  **Relationship:** source, target, semantic type, evidence, and confidence / provenance.

### V1 明确不包含 | Explicit V1 Non-goals

- 完整覆盖整个 Org 的依赖关系图谱。  
  Full-Org dependency graph completeness.
- 完整 Runtime Execution Trace。  
  Complete runtime execution tracing.
- 自动推断所有业务执行链路。  
  Automatic inference of every business execution chain.
- 自动执行或修改业务流程。  
  Automated execution or modification of business processes.

**完成标准 | Exit Criteria**

- 支持的 Resource 与 Relationship 类型有明确文档。  
  Supported Resource and Relationship types are documented.
- Object / Field 入口能够展示关联资源及可追溯证据。  
  Object / Field entry points display related resources with traceable evidence.
- 已确认、推断与可能存在的关系可以区分。  
  Confirmed, inferred, and possible relationships are distinguishable.
- 至少通过一个真实 Org 场景验证模型及其边界。  
  At least one real-Org scenario validates the model and its limitations.

---

## Phase 6 — 统一 Org 分析 | Unified Org Analysis

**目标 | Goal**

通过组合两大核心分析支柱，形成复合分析价值。

Create compound analytical value by combining the two core analysis pillars.

### Permission × Reference | 权限与资源关系联合分析

围绕用户希望完成的操作，将操作涉及的资源路径与用户有效的 Object、Field、Record Access 结合起来。不仅解释访问为何受限，也帮助用户理解相关资源参与了什么流程，以及哪些权限约束可能产生影响。

For a user-facing operation, connect the resources involved in that operation with the user's effective Object, Field, and Record Access. Explain not only why access is constrained, but also how relevant resources participate in the process and which permission constraints may matter.

### Cross-Org Analysis | 跨 Org 分析

在 Multi-Org 基础上逐步支持比较：

Build on the Multi-Org foundation to compare:

- 等价用户或角色的权限差异。  
  Permission differences for equivalent users or roles.
- Metadata / Resource Relationship 差异。  
  Metadata and Resource Relationship differences.
- Sandbox 与 Production 之间的环境漂移。  
  Environment drift between Sandbox and Production.
- 跨 Org 的权限与资源联合变化。  
  Combined permission and resource changes across Orgs.

### 从分析到决策 | From Analysis to Decision

围绕用户的问题组织分析结果、证据、影响，以及后续调查或操作方向。Wye 的职责是帮助用户做好判断，而不是在缺少业务上下文时替用户做业务决策。

Organize results around the user's question, evidence, impact, and possible next investigation or operation. Wye should prepare users to make decisions, not make business decisions on their behalf without the necessary business context.

本阶段属于长期产品方向，不是前述阶段交付的前置条件。

This phase represents a longer-term product direction and is not a prerequisite for delivering the earlier phases.

---

## 建议执行顺序 | Recommended Execution Order

1. 优先完成 Phase 1，尤其是 #1、#2、#3，确保多 Org 上下文与缓存可信。  
   Complete Phase 1 first, especially #1, #2, and #3, to establish trustworthy Multi-Org context and cache behavior.
2. 尽早建立 Phase 2 的测试与构建门禁，保护后续修复与功能扩展。  
   Establish Phase 2 test and build gates early to protect subsequent fixes and feature work.
3. 完成 Permission V1 的访问归因与真实 Org 验证。  
   Complete Permission V1 access attribution and real-Org validation.
4. 以具体 Metadata 案例设计 Reference V1，再实现最小模型。  
   Design Reference V1 around concrete metadata examples before implementing its minimal model.
5. 在底层模型可信后，再推进高级 What-if 与统一分析。  
   Pursue advanced What-if and unified analysis only after the underlying models are trustworthy.

---

## 里程碑 | Milestones

| 里程碑 Milestone | 包含阶段 Phases | 交付意义 Release Meaning |
|---|---|---|
| M1 — Reliable Runtime / 可靠运行时 | Phase 1–2 | 安全、Org 上下文一致且具备测试基础的运行环境 / A reliable, Org-consistent runtime with an engineering test foundation |
| M2 — Permission Analysis / 权限分析 | Phase 3，及部分 Phase 4 基础 / Phase 3 plus selected Phase 4 groundwork | 第一分析支柱达到可信可用 / First analysis pillar reaches trustworthy usability |
| M3 — Resource Analysis / 资源分析 | Phase 5 | 建立第二分析支柱 / Establish the second analysis pillar |
| M4 — Unified Analysis / 统一分析 | Phase 4 与 Phase 6 | 形成复合分析、模拟与跨 Org 洞察 / Compound analysis, simulation, and cross-Org insight |

---

## 范围与状态约定 | Scope and Status Principles

- Multi-Org 是运行基础，不是 Wye 的最高层产品定义。  
  Multi-Org is the runtime foundation, not the highest-level definition of Wye.
- Permission 与 Reference 是两大核心分析支柱。  
  Permission and Reference are the two core analysis pillars.
- Tree 负责可读的结构化归因；Graph 提供复合关系分析，并应通过有意义的交互融入 Tree，而不是要求 UI 永久展示完整大图。  
  Tree provides readable, structured attribution; Graph provides compound relationship analysis and should be surfaced through meaningful interactions within the Tree rather than requiring a permanently displayed full graph.
- 当前 Reference 实现属于预留 UI / Manager 入口，不代表关系分析引擎已经交付。  
  The current Reference implementation is a reserved UI / Manager entry point, not a delivered relationship-analysis engine.
- 源码中存在 Graph 算法，不等于 What-if 或 Impact Analysis 已经完成集成并通过验证。  
  The presence of Graph algorithms in source code does not mean What-if or Impact Analysis is integrated and validated.
- 不应仅凭 Class、Method、UI 入口或算法存在，就宣称某项能力已经完成。完成意味着集成、验证，并明确结果的适用边界。  
  A Class, Method, UI entry point, or algorithm alone is not evidence that a capability is complete. Completion requires integration, validation, and clearly defined output boundaries.
