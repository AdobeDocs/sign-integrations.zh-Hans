---
title: Coupa安装指南
description: 启用Adobe Sign与Coupa BSM Suite集成的安装指南
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 12c91be5-afec-4918-a8fc-ceb33bedf98b
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 7%

---

# [!DNL Coupa] 安装指南{#coupa-installation-guide}

[**联系 Adobe Sign 技术支持**](https://adobe.com/go/adobesign-support-center_cn)

## 概览 {#overview}

本文档介绍如何配置Adobe Sign帐户以集成 [!DNL Coupa BSM Suite] 以获取签名。

先决条件:

* 订购Adobe Sign Enterprise， [Adobe Sign Developer Edition](https://www.adobe.com/sign/developer-form.html)或 [Adobe Sign Enterprise试用版](https://www.adobe.com/sign/business.html)
* Adobe Sign管理员访问权限
* [!DNL Coupa BSM Suite] 标准或高级实例

完成集成的高级步骤包括：

* 配置Adobe Sign组以用于 [!DNL Coupa BSM Suite]
* Connect [!DNL Coupa BSM Suite] 到Adobe Sign
* 创建用于通知 [!DNL Coupa BSM Suite] 实例

## 配置Adobe Sign组 [!DNL Coupa BSM Suite] {#configure-adobe-sign-for-coupa}

要专门使用Adobe Sign for [!DNL Coupa] 在组织内，管理员必须专门为 [!DNL Coupa BSM Suite] 用法。 此Adobe Sign组应具有一个充当服务帐户的组管理员用户帐户。 由于此服务帐户用于所有签名请求，因此应保持匿名，例如， `Legal@xyz.com`, `Purchasing@xyz.com`或 `CoupaCLM@xyz.com`，而不是个人，例如 `Bob.Smith@xyz.com`的

### 在Adobe Sign中创建组和用户 {#create-sign-user-group}

要在 Adobe Sign 中创建用户，请执行以下操作：

1. 以帐户管理员的身份登录到 Adobe Sign。
1. 导航至 **[!UICONTROL 帐户]** > **[!UICONTROL 用户]**&#x200B;的
1. 如需创建新用户，请单击 ![加号图标图像](images/icon_plus.png) 图标。
1. 在打开的对话框中，提供新用户详细信息：

   1. 提供您可以访问的功能性电子邮件。

      * 此用户建立并维护OAuth关系。
      * 电子邮件地址必须是用于验证的实际地址。
   1. 输入适当的值 [!UICONTROL 名字] 和 [!UICONTROL 姓氏]的
   1. 在 [!UICONTROL 主要组] 字段，选择 **[!UICONTROL 为此用户创建新组]**&#x200B;的
   1. 在 [!UICONTROL 新组名称] 字段，提供直观的组名称，例如 *[!DNL Coupa BSM Suite]*&#x200B;的

   ![“创建用户”面板](images/create-user.png)

1. 选择 **[!UICONTROL 保存]**&#x200B;的

   保存详细信息后， [!UICONTROL 用户] 页面会显示新用户的 [!UICONTROL 已创建] 状态。

   ![新创建用户的视图](images/post-user-creation.png)

   在 [!UICONTROL 已创建] 状态指示用户尚未验证其电子邮件地址。

1. 要验证电子邮件地址，请执行以下操作：
   1. 登录到新用户的电子邮件。
   2. 找到“欢迎使用 Adobe Sign”电子邮件. 如果需要，请检查垃圾文件夹。
   3. 单击写有&#x200B;**[!UICONTROL 请单击此处以设置您的密码]**&#x200B;的地方
   4. 设置密码。

   验证电子邮件地址后，用户的状态将从 [!UICONTROL 已创建] 来 [!UICONTROL 活动]的

   ![新激活的用户的图像](images/active-user.png)

### 定义进行身份验证的用户 {#define-authenticating-user}

创建组以及组中的用户后，您必须将该用户设置为“组管理员”。

要在 [!DNL Coupa BSM Suite] 组：

1. 导航至 [!UICONTROL 用户] 页面（如果还不存在）。
2. 双击该用户。

   此时会打开 [!UICONTROL 编辑] 页面。

3. 在组成员资格部分下，选择 **[!UICONTROL 组管理员]** 和 **[!UICONTROL 可以发送]** 选项。
4. 取消选择 **[!UICONTROL 用户是帐户管理员]** 和 **[!UICONTROL 用户可以签署文档]** 选项。
5. 单击&#x200B;**[!UICONTROL 保存]**。

   ![用户设置的图像](images/user-settings.png)

## 配置 [!DNL Coupa BSM Suite] 实例 {#configure-coupa}

要完成 [!DNL Coupa BSM Suite ] 实例和Adobe Sign，服务之间必须建立信任关系。

要配置 [!DNL Coupa BSM Suite]:

1. 连接您的 [!DNL Coupa BSM Suite] 实例到您在上面创建的Adobe Sign服务帐户。
1. 创建Adobe Sign Webhook实例以通知您的Coupa BSM Suite实例有关协议更新的信息。

有关如何连接 [!DNL Coupa BSM Suite] 以及如何创建和注册webhook，请参阅 [Adobe Sign Coupa BSM套件实例支持文档](https://success.coupa.com/Support/Docs/Power_Apps/CLM_Standard/Signing_and_Approvals/Enable_E-Signatures_Through_Adobe_Sign_and_DocuSign){target=&quot;_blank&quot;}。

## 创建 [!DNL Webhook] 在Adobe Sign {#create-webhook}

Coupa CLM集成使用Adobe Sign的Webhook通知来发送有关协议状态的更新。 请务必完成Webhook设置，否则发送以供签名的协议会保持不完整，或者已签名的协议不会发送回Coupa CLM。

要在Adobe Sign中创建Webhook，请执行以下操作：

1. 例如，使用上面创建的组管理员用户登录到Adobe Sign `coupaclm@MyDomain.com`的

1. 导航至 **组** > **Webhook**&#x200B;的

   ![用户设置的图像](images/webhook-login.png)

1. 要创建新连接，请选择 ![加号图标图像](images/icon_plus.png) 图标。

1. 在打开的“创建”对话框中，填写必填字段。

   **注意：** 您需要从Coupa获取Webhook处理程序的Url。

   ![用户设置的图像](images/webhook-create.png)

1. 选择所需的通知参数。

1. 选择 **保存**&#x200B;的

## 支持 {#support}

### [!DNL Coupa BSM Suite] 支持 {#coupa-support}

[!DNL Coupa BSM Suite ] 是集成所有者，对于有关集成范围、功能请求或集成的日常功能的问题，您应成为第一个联系点。

如有任何疑问，请联系 [Coupa支持](https://success.coupa.com/Support/Welcome_to_Coupa_Support){target=&quot;_blank&quot;}。

### Adobe Sign支持 {#adobe-sign-support}

Adobe Sign是集成合作伙伴，如果集成无法获得签名，或者等待签名的通知失败，应与它联系。

要获得有关使用或配置Adobe Sign的帮助，请联系您的客户成功经理(CSM)或联系 [Adobe Sign支持](https://adobe.com/go/adobesign-support-center)的

Adobe Sign管理员还可以打开票证并通过帮助(?)获得支持 在Adobe Sign门户右上角。

![Adobe Sign门户帮助的图像](images/sign-portal-help.png)
