---
title: Workday安装指南
description: 启用Adobe Sign与Workday集成的安装指南
uuid: 56478222-fe66-4fa5-aac3-0ecdf2863197
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 29d55a25-6e2f-4c59-ae7c-c21bb82cecba
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 8f12b524-2123-45d4-98d5-b2b23580a5ea
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 0%

---

# [!DNL Workday] 安装指南{#workday-installation-guide}

[**联系Adobe Sign支持**](https://adobe.com/go/adobesign-support-center)

## 概述 {#overview}

本文档介绍如何将Adobe Sign集成到 [!DNL Workday] 租户。 要在 [!DNL Workday]，您需要了解如何创建和修改 [!DNL Workday] 例如：

* 业务流程框架
* 租户设置和配置
* 报告和 [!DNL Workday] studio集成

完成集成的高级步骤包括：

* 在Adobe Sign中激活您的管理帐户（仅限新客户）
* 在Adobe Sign中配置组以容纳 [!DNL Workday] 集成用户
* 建立OAuth关系 [!DNL Workday] 和Adobe Sign

## 激活您的Adobe Sign帐户 {#activating-your-adobe-sign-account}

已建立帐户的现有客户可跳至 [配置Adobe Sign [!DNL Workday]](#config) 问题。

对于不熟悉Adobe Sign并且没有预先登录的客户，Adobe入门专家将为您的(在Adobe Sign中)帐户提供 [!DNL Workday]的 完成后，您会收到确认电子邮件，如下所示。

![来自Adobe Sign的欢迎电子邮件图像](images/welcome-email-2020.png)

您需要按照电子邮件中的指示，初始化您的帐户并访问您的Adobe Sign [!UICONTROL 主页] 页面。

![Adobe Sign Dashboard页面](images/classic-home.png)

## 配置Adobe Sign [!DNL Workday] {#config}

要为 [!DNL Workday]，您需要在Adobe Sign系统中生成以下两个专用对象：

* **A [!DNL Workday] 编组**: [!DNL Workday] 需要在Adobe Sign帐户内有一个专用的“组”才能启用集成功能。 Adobe Sign组仅用于控制 [!DNL Workday] Adobe Sign的使用。 任何其他潜在用途（例如Salesforce.com或Arriba）都不会受到影响。 在中禁止显示电子邮件通知 [!DNL Workday] 组，以使 [!DNL Workday] 用户仅在其个人帐户的 [!DNL Workday] 收件箱。

* **用于保存集成密钥的进行身份验证的用户**:A [!DNL Workday] 组必须只有一个组级别管理员，他是集成密钥的权威持有者。 我们建议管理员使用功能性电子邮件地址，例如 `HR@MyDomain.com` 用户不再使用个人电子邮件，从而降低将来禁用用户并进而禁用集成的风险。

### 在Adobe Sign中创建用户和组 {#create-a-user-and-group-in-adobe-sign}

要在Adobe Sign中创建用户，请执行以下操作：

1. 以帐户管理员的身份登录Adobe Sign。
1. 导航至 **[!UICONTROL 帐户]** > **[!UICONTROL 用户]**&#x200B;的
1. 单击 ![加号图标图像](images/icon_plus.png) 以创建新用户。

   ![用于创建新用户的导航路径图像](images/navigate-to-group-unbranded.png)

1. 在打开的对话框中，提供新用户详细信息：

   * 提供您可以访问的功能性电子邮件。
   * 输入适当的名字和姓氏值。
   * 选择 **[!UICONTROL 为此用户创建新组]** 从用户组。
   * 提供 **[!UICONTROL 新组名称]** 使用直观名称，例如 *[!DNL Workday]*&#x200B;的

   ![“创建用户”面板](images/create-user.png)

1. 单击 **[!UICONTROL 保存]**&#x200B;的

   它会带您回到 [!UICONTROL 用户] 页面列出了新用户 **[!UICONTROL 已创建]** 状态。

   ![新创建用户的视图](images/post-user-creation.png)

要验证状态为“已创建”的用户的电子邮件地址，请执行以下操作：

1. 登录到新用户的电子邮件。
2. 查找“欢迎使用Adobe Sign”电子邮件。
3. 单击显示文字的位置 **[!UICONTROL 单击此处设置密码]**&#x200B;的
4. 设置密码。

验证电子邮件地址后，用户的状态将从 [!UICONTROL 已创建] 来 [!UICONTROL 活动]的

![新激活的用户的图像](images/actived-users-575.png)

### 定义进行身份验证的用户 {#define-the-authenticating-user}

要在 [!DNL Workday] 组：

1. 导航至 [!UICONTROL 用户] 页面（如果还不存在）。
2. 在 [!DNL Workday] 组。

   这将打开 [!UICONTROL 编辑] 页面。

3. 请查看 **[!UICONTROL 组管理员]**&#x200B;的
4. 单击 **[!UICONTROL 保存]**&#x200B;的

![](images/user-permissions-edit1-575.png)

## 配置 [!DNL Workday] 租户 {#configure-workday}

要完成 [!DNL Workday] 租户和Adobe Sign，我们需要在服务之间建立信任关系。 完成后，我们可以添加审阅文档步骤，以通过Adobe Sign启用签名流程。

>[!NOTE]
>
>Adobe Sign在整个 [!DNL Workday] 环境。

要建立信任关系，请执行以下操作：

1. 登录到 [!DNL Workday] 作为帐户管理员。
1. 打开 **[!UICONTROL 编辑租户设置 — 业务流程]** 页面。
1. 找到 [!UICONTROL 电子签名配置] 部分：

   ![](images/esignature_configurations.png)

1. 单击 **[!UICONTROL 使用Adobe]**&#x200B;的

   这会启动OAuth2.0身份验证序列。

1. 当系统询问时，提供您之前创建的Adobe Sign组管理员的凭据。
1. 批准访问Adobe Sign。

>[!NOTE]
>
>在继续之前，请确保完全注销任何其他Adobe Sign实例。

连接后，选中“Adobe配置已启用”复选框，然后您就可以开始搭配使用Adobe Sign [!DNL Workday]的

### 配置审阅文档步骤 {#configure-review}

用于审阅文档步骤的文档可以为下列任一项：

* 静态文档
* 由同一业务流程内的“生成文档”步骤生成的文档
* 使用 [!DNL Workday] 报告设计器

您可以添加这些文档中的任何一个 [Adobe文本标记](https://adobe.com/go/adobesign_text_tag_guide) 以控制“Adobe签名”特定组件的外观和位置。 必须在业务流程定义中指定文档源。 在执行业务流程时无法上载临时文档。

配合使用Adobe Sign和审阅文档步骤的独特之处在于，它能够提供序列化的签名者组。 这样，您便可以指定按顺序签名的基于角色的组。 Adobe Sign不支持并行签名组。

要获得配置审阅文档步骤方面的帮助，请参阅 [快速入门指南](https://adobe.com//go/adobesign_workday_quick_start){target="_blank"}的

## 支持 {#support}

### [!DNL Workday] 支持 {#workday-support}

[!DNL Workday] 是集成所有者，对于有关集成范围的问题、功能请求或集成的日常功能问题，您应当成为第一个联系点。

您可以参考以下内容 [!DNL Workday] 有关如何解决集成问题和生成文档的社区文章：

* [电子签名集成疑难解答](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [审阅文档步骤](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [动态文档生成](https://community.workday.com/saml/login?destination=/articles/176443)
* [聘用文档生成提示](https://community.workday.com/node/183242)

### Adobe Sign支持 {#adobe-sign-support}

Adobe Sign是集成合作伙伴，如果集成无法获取签名，或挂起的签名通知失败，应与它联系。

Adobe Sign客户应联系其客户成功经理(CSM)以获得支持。 或者，Adobe可通过电话联系技术支持：1-866-318-4100，等待产品列表，然后输入：4和2（根据提示）。

* [添加Adobe文本标记到文档](https://adobe.com/go/adobesign_text_tag_guide)
* [查看文档配置和示例](https://www.adobe.com//go/adobesign_workday_quick_start)

## 常见问题 {#faq}

### 为什么状态未在内部更新 [!DNL Workday] 即使文档已完全签名？ {#why-is-the-status-not-being-updated-within-workday-even-the-document-is-fully-signed}

中的文档状态 [!DNL Workday] 如果候选人未单击“[!UICONTROL 提交]”按钮。

根据 [!DNL Workday] 任务检查电子签名签名状态：要开始此过程，用户可以提交关联的收件箱任务。

根据 [!DNL Workday] 发展：仅当用户在签名文档后提交收件箱任务时，原始签名才会完成此过程。 签名后，iframe将关闭，用户将重定向到相同的任务，在该任务中，用户可以 [!UICONTROL 提交] 按钮来完成此过程。
