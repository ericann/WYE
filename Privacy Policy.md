# Privacy Policy for Wye — Salesforce Workspace
**Last Updated:** [Oct 31 2026]
**Effective Date:** [Oct 31 2026]

This Privacy Policy explains how **Wye — Salesforce Workspace** ("Wye", "the Extension", "we", "us", or "our") handles your information. Wye is committed to protecting your privacy and ensuring you have a secure experience while diagnosing Salesforce permissions.
本隐私政策解释了 **Wye — Salesforce Workspace**（以下简称“Wye”或“本扩展”）如何处理您的信息。Wye 致力于保护您的隐私，并确保您在诊断 Salesforce 权限时享有安全的体验。

---

## 1. Information We Collect and Access
**1. 我们收集和访问的信息**

### 1.1 Salesforce Authentication Data
**Salesforce 身份验证数据**
Wye uses the **OAuth 2.0 PKCE (Proof Key for Code Exchange)** flow to authenticate you securely via Salesforce. We do not collect, see, or store your Salesforce username or password. 
Wye 使用 **OAuth 2.0 PKCE** 标准流程通过 Salesforce 进行安全身份验证。我们绝不会收集、查看或存储您的 Salesforce 用户名或密码。

We temporarily receive an **Access Token** and a **Refresh Token** to make API calls on your behalf. These tokens are stored securely in your browser's local extension storage (`chrome.storage.local`) on your device. Tokens are never transmitted to any external server controlled by us.
我们会临时接收 **Access Token**（访问令牌）和 **Refresh Token**（刷新令牌）以代表您发起 API 调用。这些令牌安全地存储在您设备本地的浏览器扩展存储（`chrome.storage.local`）中，绝不会被传输到我们控制的任何外部服务器。

### 1.2 Salesforce Metadata & Permission Data
**Salesforce 元数据与权限数据**
To provide our core features (User Access, Resource Exposure, Record Exposure, etc.), Wye fetches metadata (e.g., profiles, permission sets, object/field permissions) and record-sharing information from your Salesforce Org via official APIs.
为了提供核心功能（用户权限分析、资源暴露、记录暴露等），Wye 通过官方 API 从您的 Salesforce 组织获取元数据（如配置文件、权限集、对象/字段权限）以及记录共享信息。

**Data Processing:** All data fetching and calculation are processed **entirely locally in your browser**. We do not operate any backend servers. No data is uploaded, cached, or stored outside your local device.
**数据处理原则：** 所有数据获取和计算均**完全在您的浏览器本地**进行。我们不运营任何后端服务器。没有任何数据会被上传、缓存或存储在您的本地设备之外。

---

## 2. How We Use Your Information
**2. 我们如何使用您的信息**

We use the accessed data strictly to:
- Authenticate your Salesforce session securely.
- Calculate and visualize the permission trees, object/field access, and record-level access within the Extension's sidebar.
我们严格仅将访问的数据用于：
- 安全地验证您的 Salesforce 会话。
- 在扩展侧边栏内计算并可视化权限树、对象/字段访问权限以及记录级访问权限。

**Limited Use Commitment:** Wye's use of data obtained from Salesforce APIs strictly adheres to the [Chrome Web Store User Data Policy](https://developer.chrome.com/docs/webstore/program-policies/user-data-faq), including the **Limited Use** requirements. Your data is only used to provide the visible features of the Extension and is never used for advertising, profiling, or sold to third parties.
**有限使用承诺：** Wye 对从 Salesforce API 获取的数据的使用严格遵守 Chrome 应用商店的用户数据政策，包括**有限使用 (Limited Use)** 要求。您的数据仅用于提供本扩展的可见功能，绝不用于广告、用户画像分析或出售给第三方。

---

## 3. Network Access & Data Sharing
**3. 网络访问与数据共享**

We **do not** sell, trade, or transfer your data to any third parties. 
我们**绝不会**向任何第三方出售、交易或转让您的数据。

To ensure transparency, the Extension's network requests are restricted exclusively to official Salesforce domains to execute SOQL queries and metadata retrieval:
为了确保透明度，本扩展的网络请求受到严格限制，仅向官方 Salesforce 域名发起 SOQL 查询和元数据检索：
- `https://*.salesforce.com/*`
- `https://*.force.com/*`

---

## 4. Data Retention
**4. 数据保留**

**Local Session:** Any metadata fetched is retained only for the duration of the active analysis session in your browser's memory. It is automatically discarded when the browser tab is closed, the side panel is closed, or the session expires.
**本地会话：** 任何获取的元数据仅保留在浏览器内存中以供当前分析会话使用。当浏览器标签页关闭、侧边栏关闭或会话过期时，这些数据将自动销毁。

**Zero Server Storage:** Because there is no backend, no database exists to store your organizational data or permission structures.
**零服务器存储：** 由于没有后端，不存在任何数据库来存储您的组织数据或权限结构。

---

## 5. Security
**5. 安全性**

We implement industry-standard security measures:
- **OAuth 2.0 PKCE:** Prevents authorization code interception attacks.
- **Zero Backend Architecture:** Eliminates the risk of data breaches on a central server.
- **Local Processing:** Keeps sensitive Salesforce configuration data within your controlled environment.
我们实施行业标准的安全措施：
- **OAuth 2.0 PKCE：** 防止授权码拦截攻击。
- **零后端架构：** 消除中央服务器数据泄露的风险。
- **本地处理：** 将敏感的 Salesforce 配置数据保留在您受控的环境内。

---

## 6. Your Control and Data Subject Rights
**6. 您的控制权与数据主体权利**

**Revoking Access:** You can revoke Wye's access to your Salesforce Org at any time. To do so, log into Salesforce, go to **Setup** > **Connected Apps OAuth Usage**, and click "Revoke" next to Wye. Alternatively, you can uninstall the Extension.
**撤销访问权：** 您可以随时撤销 Wye 对您的 Salesforce 组织的访问权限。请登录 Salesforce，前往**设置 (Setup)** > **连接的应用程序 OAuth 使用情况 (Connected Apps OAuth Usage)**，在 Wye 旁边点击“撤销 (Revoke)”。或者，您也可以直接卸载本扩展。

**GDPR & Data Subject Rights:** Since Wye processes data entirely in-memory and does not transmit it to any central server or maintain a database of personal data, the traditional data controller/processor relationship does not apply to your Salesforce data. If you have any concerns, please contact us.
**GDPR 与数据主体权利：** 由于 Wye 完全在内存中处理数据，不将其传输到任何中央服务器，也不维护个人数据库，因此传统的数据控制者/处理者关系不适用于您的 Salesforce 数据。如果您有任何疑虑，请联系我们。

---

## 7. Changes to This Privacy Policy
**7. 隐私政策的变更**

We may update this Privacy Policy from time to time. We will notify you of any changes by updating the "Last Updated" date at the top of this document.
我们可能会不时更新本隐私政策。我们将通过更新本文档顶部的“最后更新”日期来通知您任何变更。

---

## 8. Contact Us
**8. 联系我们**

If you have any questions, concerns, or feedback regarding this Privacy Policy or the Extension, please contact the developer at:
如果您对本隐私政策或本扩展有任何疑问、疑虑或反馈，请通过以下方式联系开发者：

**Email:** [yxeysy@gmail.com]
