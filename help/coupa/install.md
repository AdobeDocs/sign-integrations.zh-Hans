---
title: 《库帕安装指南》
description: 支持Adobe Sign与Coupa BSM Suite集成的安装指南
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 12c91be5-afec-4918-a8fc-ceb33bedf98b
source-git-commit: 623307e86f1b32edfbfa59dbd636ff74a6d09b62
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 7%

---

# [!DNL Coupa] 安装指南{#coupa-installation-guide}

[**联系 Adobe Sign 技术支持**](https://adobe.com/go/adobesign-support-center_cn)

## 概览 {#overview}

本文档介绍如何配置Adobe Sign帐户以集成[!DNL Coupa BSM Suite]实例以获取签名。

先决条件:

* 订阅Adobe Sign Enterprise、[Adobe Sign Developer Edition](https://www.adobe.com/sign/developer-form.html)或[Adobe Sign Enterprise Trial](https://www.adobe.com/sign/business.html)
* Adobe Sign管理员访问
* [!DNL Coupa BSM Suite] 标准或高级实例

完成集成的高级步骤包括：

* 配置Adobe Sign组以与[!DNL Coupa BSM Suite]一起使用
* 将[!DNL Coupa BSM Suite]连接到Adobe Sign
* 创建Adobe Sign Webhook以通知[!DNL Coupa BSM Suite]实例

## 为[!DNL Coupa BSM Suite]配置Adobe Sign组 {#configure-adobe-sign-for-coupa}

要在组织内为[!DNL Coupa]专用使用Adobe Sign，管理员必须为[!DNL Coupa BSM Suite]使用专门创建Adobe Sign组。 此Adobe Sign组应有一个组管理员用户帐户作为服务帐户。 由于此服务帐户用于所有签名请求，因此应将其保持为匿名，例如`Legal@xyz.com`、`Purchasing@xyz.com`或`CoupaCLM@xyz.com`，而不是个人帐户，如`Bob.Smith@xyz.com`。

### 在Adobe Sign中创建组和用户 {#create-sign-user-group}

要在 Adobe Sign 中创建用户，请执行以下操作：

1. 以帐户管理员的身份登录到 Adobe Sign。
1. 导航到&#x200B;**[!UICONTROL 帐户]** > **[!UICONTROL 用户]**。
1. 要创建新用户，请单击![加号图标图像](images/icon_plus.png)图标。
1. 在打开的对话框中，提供新用户详细信息：

   1. 提供可访问的功能性电子邮件。

      * 此用户建立并维护OAuth关系。
      * 电子邮件地址必须是实际的地址才能进行验证。
   1. 为[!UICONTROL 名字]和[!UICONTROL 姓氏]输入适当的值。
   1. 在[!UICONTROL 主组]字段中，选择&#x200B;**[!UICONTROL 为此用户]**&#x200B;创建新组。
   1. 在[!UICONTROL 新建组名称]字段中，提供直观的组名称，如&#x200B;*[!DNL Coupa BSM Suite]*。

   ![“创建用户”面板](images/create-user.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

   保存详细信息后，[!UICONTROL 用户]页将显示状态为[!UICONTROL CREATED]的新用户。

   ![新创建用户的视图](images/post-user-creation.png)

   [!UICONTROL CREATED]状态指示用户尚未验证其电子邮件地址。

1. 要验证电子邮件地址，请执行以下操作：
   1. 登录到新用户的电子邮件。
   2. 找到“欢迎使用 Adobe Sign”电子邮件. 如果需要，检查垃圾邮件/垃圾邮件文件夹。
   3. 单击写有&#x200B;**[!UICONTROL 请单击此处以设置您的密码]**&#x200B;的地方
   4. 设置密码。

   验证电子邮件地址后，用户的状态从[!UICONTROL CREATED]更改为[!UICONTROL ACTIVE]。

   ![新激活用户的图像](images/active-user.png)

### 定义验证用户 {#define-authenticating-user}

在该组中创建组和用户后，必须使用户成为“组管理员”。

要提升[!DNL Coupa BSM Suite]组中的新用户，请执行以下操作：

1. 导航到[!UICONTROL 用户]页（如果尚未）。
2. 双击用户。

   它打开用户权限的[!UICONTROL 编辑]页。

3. 在“组成员身份”部分下，选择&#x200B;**[!UICONTROL 组管理员]**&#x200B;和&#x200B;**[!UICONTROL 可以发送]**&#x200B;选项。
4. 取消选择“**[!UICONTROL 用户是帐户管理员]**”和“**[!UICONTROL 用户可以签名文档]**”选项。
5. 单击&#x200B;**[!UICONTROL 保存]**。

   ![用户设置的图像](images/user-settings.png)

## 配置[!DNL Coupa BSM Suite]实例 {#configure-coupa}

要完成[!DNL Coupa BSM Suite ]实例与Adobe Sign之间的连接，必须在服务之间建立信任关系。

配置[!DNL Coupa BSM Suite]:

1. 将[!DNL Coupa BSM Suite]实例连接到您在上面创建的Adobe Sign服务帐户。
1. 创建Adobe Sign Webhook实例，以通知Coupa BSM Suite实例有关协议的更新。

有关如何连接[!DNL Coupa BSM Suite]以及如何创建和注册Webhook的详细信息，请参阅[Adobe Sign Coupa BSM Suite实例支持文档](https://success.coupa.com/Support/Docs/Power_Apps/CLM_Standard/Signing_and_Approvals/Enable_E-Signatures_Through_Adobe_Sign_and_DocuSign){target=&quot;_blank&quot;}。

## 在Adobe Sign中创建[!DNL Webhook] {#create-webhook}

Coupa CLM集成使用来自Adobe Sign的Webhook通知发送有关协议状态的更新。 完成Webhook设置，否则发送以供签名的协议将保持不完整，或者已签名的协议不会返回到Coupa CLM中，这一点非常重要。

在Adobe Sign中创建网页挂接：

1. 使用上面创建的组管理员用户登录Adobe Sign，例如`coupaclm@MyDomain.com`。

1. 导航到&#x200B;**组** > **Webhooks**。

   ![用户设置的图像](images/webhook-login.png)

1. 要创建新连接，请选择![加号图标图像](images/icon_plus.png)图标。

1. 在打开的“创建”对话框中，填写必填字段。

   **注意：** 您需要从Coupa获取网页钩子处理程序的Url。

   ![用户设置的图像](images/webhook-create.png)

1. 选择所需的通知参数。

1. 选择&#x200B;**保存**。

## 支持 {#support}

### [!DNL Coupa BSM Suite] 支持 {#coupa-support}

[!DNL Coupa BSM Suite ] 是集成所有者，如果您对集成范围、功能请求或集成日常功能中的问题有任何疑问，请首先联系您。

对于任何查询，请联系[Coupa Support](https://success.coupa.com/Support/Welcome_to_Coupa_Support){target=&quot;_blank&quot;}。

### Adobe Sign支持 {#adobe-sign-support}

Adobe Sign是集成合作伙伴，如果集成无法获取签名，或者挂起签名通知失败，应与它联系。

要获得有关使用或配置Adobe Sign的帮助，您可以联系您的客户成功经理(CSM)或联系[Adobe Sign支持](https://adobe.com/go/adobesign-support-center)。

Adobe Sign管理员还可以打开票证并通过帮助(?)获取支持 在Adobe Sign门户的右上角。

![Adobe Sign门户帮助的图像](images/sign-portal-help.png)
