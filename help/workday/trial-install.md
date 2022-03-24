---
title: Workday 试用版安装
description: 适用于 Adobe Sign 试用版帐户的 Workday 安装指南
uuid: 0c51f329-b7c1-44a2-88a3-670be7673747
products: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 63ed2d5b-9d82-4f87-97e1-2dde23501e89
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: beafe6c0-262f-4f5b-9315-a023a4eef4a2
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 39%

---

# [!DNL Workday] 试用版安装{#workday-trial-installation}

## 概览 {#overview}

本文档旨在帮助您 [!DNL Workday] 客户了解如何使用Adobe Sign激活试用帐户，然后将其集成到 [!DNL Workday] 租户。 要在 [!DNL Workday]，您必须知道如何创建和修改 [!DNL Workday] 例如：

* 业务流程框架
* 租户设置和配置
* 报告和 [!DNL Workday] Studio集成

**注释**:如果您已经拥有Adobe Sign帐户，则不必开始试用。 您可以联系您的客户成功经理以请求 [!DNL Workday] 集成。

完成集成的高级步骤如下：

* 通过 Adobe Sign 激活您的试用版帐户
* 在Adobe Sign中生成集成密钥
* 将集成密钥安装到 [!DNL Workday] 租户

## 激活您的Adobe Sign试用帐户 {#activate-sign-trial-account}

要请求Adobe Sign 30天试用版，您必须填写以下内容 [注册表](https://land.echosign.com/esign-trial-workday-registration.html)的

**注释**:我们强烈建议您使用有效的功能性电子邮件地址来创建试用版，而不是创建临时电子邮件。 您必须访问此电子邮件地址才能验证帐户，因此地址必须有效。

![试用版申请表单](images/trial-land.png)

在一个工作日内，Adobe Sign入职专家为您的帐户(在Adobe Sign中)提供 [!DNL Workday]的 完成后，您会收到确认电子邮件，如下所示。

![来自 Adobe Sign 的欢迎电子邮件](images/welcome-email-2020.png)

初始化您的帐户并访问您的Adobe Sign [!UICONTROL 主页] 页面，请按照电子邮件中的说明进行操作。

![Adobe Sign功能板](images/classic-home.png)

## 生成集成密钥 {#generate-an-integration-key}

对于新安装，您必须在Adobe Sign中生成集成密钥，然后将其输入到 [!DNL Workday]的 此密钥可验证Adobe Sign和 [!DNL Workday] 彼此信任并共享内容的环境。

要在 Adobe Sign 中生成集成密钥，请执行以下操作：

1. 在 Adobe Sign 中以管理员登录.
1. 导航至 **[!UICONTROL **帐户]** > **[!UICONTROL 个人首选项]** > **[!UICONTROL 访问令牌**]**&#x200B;的
1. 单击窗口右侧的&#x200B;**带圆圈的加号图标.**

   它会打开 [!UICONTROL 创建集成密钥] 界面。

   ![到访问令牌页面的导航图像](images/navigate-to-group-accesstokens.png)

1. 为您的密钥提供一个直观的名称，例如 [!DNL Workday]的

   集成密钥必须启用了以下元素：

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_read
   * library_read

   ![“创建集成密钥”面板](images/create-integration-key-575.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

   [!UICONTROL 访问令牌]页面将公开，以显示在您的帐户中安排的密钥。

1. 单击为创建的密钥定义 [!DNL Workday]的

   [!UICONTROL 集成密钥]链接在定义的顶部公开.

1. 单击&#x200B;**[!UICONTROL 集成密钥]**&#x200B;链接.

   它公开集成密钥。

   ![集成密钥链接](images/integration-key.png)

1. 复制此密钥，并将其保存在一个安全的地方以供后续步骤使用.
1. 单击&#x200B;**[!UICONTROL 确定]**.

   ![“集成密钥”面板](images/copy-the-key-575.png)

## 配置 [!DNL Workday] 租户 {#configuring-the-workday-tenant}

### 安装集成密钥 {#install-the-integration-key}

将集成密钥安装到 [!DNL Workday] 租户与Adobe Sign建立信任关系。 在这种关系建立之后，任何业务流程都可以 [!UICONTROL 审阅文档步骤] 添加了启用签名流程的功能。

**注意**[!DNL Workday]：Adobe Sign 在整个 环境中被称为“Adobe Document Cloud”。

要安装集成密钥，请执行以下操作：

1. 登录到 [!DNL Workday] 作为帐户管理员。
1. 搜索并打开 **[!UICONTROL 编辑租户设置 — 业务流程]** 页面。

1. 提供以下四个字段的信息：

   * **[!UICONTROL Adobe Document Cloud Acknowledgement]**:集成的固定文本确认。

   * **[!UICONTROL Adobe Document Cloud API密钥]**:集成密钥的安装位置

   * **[!UICONTROL Adobe Document Cloud发件人电子邮件地址]**:组级别管理员在Adobe Sign中的电子邮件地址

   * **[!UICONTROL 取消文档时删除等待电子签名的文档]**:一个可选配置，用于在在中取消文档时从签名周期中删除文档 [!DNL Workday]的

   ![Adobe Sign 集成密钥的字段](images/bp-filled-torn2-575.png)

1. 接下来，完成安装：

   1. 将您的集成密钥粘贴到 [!UICONTROL Adobe Sign API 集成密钥]字段中.
   1. 将 Adobe Sign 管理员的电子邮件地址输入到 [!UICONTROL Adobe Document Cloud 发送者电子邮件地址]字段中.
   1. 单击&#x200B;**[!UICONTROL 确定]**.

   ![集成密钥字段和密钥持有者电子邮件字段](images/bp-filled-small.png)

Adobe Sign功能现在可以通过将 [!UICONTROL 审阅文档步骤] 并将其配置为使用 **[!UICONTROL eSign byAdobe]** 作为电子签名类型。

### 配置审阅文档步骤 {#configure-the-review-document-step}

用于审阅文档步骤的文档可以是静态文档；由同一业务流程内的“生成文档”步骤生成的文档；或者，使用 [!DNL Workday] 报告设计器。 所有这些文档都可通过 [Adobe 文本标记](https://adobe.com/go/adobesign_text_tag_guide_cn)进行加强，以便控制 Adobe 签名特定组件的外观和位置。文档来源必须在业务流程定义内指定。在执行业务流程时无法上载临时文档。

配合使用Adobe Sign和审阅文档步骤的独特之处在于，它能够提供序列化的签名者组。 签名者组允许您指定按顺序签名的基于角色的组。 Adobe Sign不支持并行签名组。

要获得配置审阅文档步骤方面的帮助，您可以参阅 [快速入门指南](https://adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}。

## 支持 {#support}

### [!DNL Workday] 支持 {#workday-support}

[!DNL Workday] 是集成所有者，如果您要咨询有关集成范围问题、功能请求或集成日常功能问题，请首先联系 Workday。

在 [!DNL Workday] 社区中有几篇关于如何解决集成问题和生成文档的好文章：

* [电子签名集成疑难解答](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [审阅文档步骤](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [动态文档生成](https://community.workday.com/node/176443)

* [聘用文档生成配置提示](https://community.workday.com/node/183242)

### Adobe Sign支持 {#adobe-sign-support}

Adobe Sign 是集成合作伙伴，如果集成获取签名失败或待定签名通知失败时，请联系 Adobe Sign。

Adobe Sign 客户应当联系各自的客户成功经理 (CSM) 以寻求支持。或者，Adobe可通过电话联系技术支持：1-866-318-4100;等待产品列表，然后输入：4和2（根据提示）。

* [将 Adobe 文本标记添加到文档](https://adobe.com/go/adobesign_text_tag_guide)

* [查看文档配置和示例](https://www.adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}

[**联系 Adobe Sign 技术支持**](https://www.adobe.com/go/adobesign-support-center)
