# 隐私政策 (Privacy Policy) / Privacy Policy for OrgPrism

**Last Updated / 最后更新日期:** May 23, 2024

## 1. 简介 (Introduction)

OrgPrism ("we", "our", or "the Extension") is a Chrome extension designed to help Salesforce administrators and developers analyze and visualize permission chains and metadata dependencies.

OrgPrism（“我们”或“本插件”）是一款专为 Salesforce 管理员和开发者设计的 Chrome 扩展，用于分析和可视化权限链路及元数据依赖。

We are committed to protecting your privacy. This policy explains what data we access, how it is used, and how it is secured.

我们极其重视您的隐私。本政策解释了我们会访问哪些数据、如何使用这些数据以及如何保障其安全。

## 2. 我们收集和访问的信息 (Information We Collect and Access)

To provide our core functionality, the Extension requires you to authenticate via Salesforce OAuth 2.0. By doing so, the Extension may access:

为了提供核心功能，本插件需要您通过 Salesforce OAuth 2.0 进行身份验证。在此过程中，插件可能会访问以下信息：

- **Salesforce Org Metadata（Salesforce 元数据）:** We access read-only data related to Profiles, Permission Sets, Permission Set Groups, Object Permissions, Field Permissions, and User Assignments.
  - 我们访问只读的简档、权限集、权限集组、对象权限、字段权限以及用户分配关系。

- **Salesforce Records（Salesforce 记录）:** When you explicitly query a specific Record ID, we fetch that record's sharing and ownership information.
  - 当您显式查询特定的记录 ID 时，我们会获取该记录的共享和所有权信息。

- **OAuth Token（OAuth 令牌）:** We temporarily store the access token in memory/session storage to make authorized API calls to your Org.
  - 我们会在内存或会话存储中临时保存访问令牌，以便向您的 Org 发起授权 API 调用。

**WE DO NOT COLLECT（我们绝不收集）:**

- Personal Identifiable Information (PII) such as your Salesforce password.
  - 任何个人身份信息（如您的 Salesforce 密码）。

- Standard Salesforce Data (e.g., actual business records, customer names, or sensitive data).
  - 标准业务数据（如实际的业务记录、客户姓名或敏感数据）。

- Financial information or billing details.
  - 财务信息或账单详情。

## 3. 数据的使用 (How We Use Your Data)

All accessed data is used strictly for the purpose of providing the analysis service:

所有访问的数据仅用于提供分析服务：

- To calculate and visualize permission trees (User -> Profile/PS -> Object -> Field).
  - 计算并可视化权限树。

- To detect and highlight security risks (e.g., ModifyAll or ViewAllFields permissions).
  - 检测并高亮显示安全风险（如超级权限）。

- To trace metadata dependencies (Reference Chains).
  - 追踪元数据依赖（引用链）。

## 4. 数据存储与保留 (Data Storage and Retention)

- **In-Memory Processing（内存计算）:** All permission calculations and graph processing are done in memory. We do not persist (save to a database) your Org's metadata or user data.
  - 所有权限计算和图处理均在内存中完成。我们不会持久化存储您的 Org 元数据或用户数据。

- **No Centralized Database（无中心化数据库）:** We do not maintain a central database of your Org's configuration data. Once the analysis session is closed or the token expires, the data is discarded.
  - 我们不保存您 Org 的配置数据。分析会话结束或令牌过期后，数据即被销毁。

## 5. 数据共享与披露 (Data Sharing and Disclosure)

We do not sell, trade, or rent your data to any third parties.

我们绝不向任何第三方出售、交易或出租您的数据。

We do not share your Org's data with advertisers or for any purposes unrelated to the core functionality of this Extension.

我们不会将您 Org 的数据共享给广告商，也不会将其用于与本插件核心功能无关的任何目的。

## 6. 您的控制权与撤销授权 (Your Control and Revoking Access)

You maintain full control over the OAuth access. You can revoke the Extension's access to your Salesforce Org at any time:

您完全控制着 OAuth 访问权限。您可以随时撤销插件对您 Salesforce Org 的访问权限：

- **Option 1:** Uninstall the Chrome Extension.
  - 方式一：卸载此 Chrome 扩展。

- **Option 2:** Log into your Salesforce Org -> Go to Setup -> Connected Apps OAuth Usage -> Find "OrgPrism" and click "Revoke".
  - 方式二：登录 Salesforce -> 转到设置 -> 连接的应用程序 OAuth 使用情况 -> 找到 "OrgPrism" 并点击“撤销”。

## 7. 安全性 (Security)

We use industry-standard HTTPS/TLS encryption for all data transmission between the Extension, your Salesforce Org, and our backend (if applicable).

所有在插件、您的 Salesforce Org 以及我们的后端（如有）之间传输的数据，均采用行业标准的 HTTPS/TLS 加密。

Access tokens are handled securely and are never exposed to unauthorized third parties.

访问令牌受到严格保护，绝不会暴露给未经授权的第三方。

## 8. 政策更新 (Changes to This Policy)

We may update this Privacy Policy from time to time. Any changes will be reflected on this page.

我们可能会不时更新本隐私政策。任何更改都将在此页面上反映。

## 9. 联系方式 (Contact Us)

If you have any questions about this Privacy Policy, please contact us at:

如果您对本隐私政策有任何疑问，请通过以下方式联系我们：

- **Email:** [yxeysy@gmail.com]
