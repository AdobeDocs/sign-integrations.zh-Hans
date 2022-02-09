---
title: Veeva Vault用户指南
description: Veeva Vault客户用户指南 — 关于如何使用Adobe Sign与Veeva的集成
products: Adobe Sign
content-type: reference
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 39a43637-af3f-432e-a784-8f472aa86df5
source-git-commit: e1394c24aebd1e026eb6c5a33935149f33ef8ea4
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# 适用于 [!DNL Veeva Vault]:用户指南 {#veeva-vault-user-guide}

[**联系 Adobe Sign 技术支持**](https://adobe.com/go/adobesign-support-center_cn)

本文档旨在帮助您 [!DNL Veeva Vault] 客户了解如何使用Adobe Sign for [!DNL Veeva Vault] 集成，以发送协议。

## 概览 {#overview}

Adobe Sign与 [!DNL Veeva Vault] 对于需要合法签名或可审核文档处理的任何文档，可加快获取签名或审批的过程。

发送文档进行签名的整个过程与发送电子邮件类似，因此大多数用户可轻松采用这种方式。

Adobe Sign与 [!DNL Veeva Vault] 简化并加速您的文档和签名工作流程。 通过使用集成工作流程，您可以：

* 节省了在邮寄、隔夜和传真上花费的时间和资源。
* 发送合同以进行电子签名或审批 [!DNL Veeva Vault]、访问实时合同历史记录，并查看保存的合同。
* 实时跟踪贵组织中的交易，并在查看、签署、取消或拒绝协议时获取更新。
* 使用 20 多种语言进行电子签名，并在全球 50 多个区域支持回传服务.
* 创建用于发送选项的可重用协议模板。

## 使用Adobe Sign for [!DNL Veeva Vault] {#send-sign-vault-agreement}

要使用Adobe Sign for Veeva发送协议，请执行以下操作：

1. 转到 [[!DNL Veeva Vault] 登录页](https://login.veevavault.com/) 然后输入您的用户名和密码。 这将打开Vault的主页，如下所示。

   ![](images/vault-home.png)

1. 选择 **[!UICONTROL 库]** 选项卡，然后选择 **[!UICONTROL 创建]** （位于右上角）。

   ![](images/create-library.png)

1. 选择 **[!UICONTROL 上传并继续]**&#x200B;的

1. 从本地驱动器上传任何文档。

1. 在出现的对话框中，选择 **[!UICONTROL 文字]** 作为 *[!UICONTROL 临床]* 然后选择 **[!UICONTROL 子类型]** 和 **[!UICONTROL 分类]**，如果需要。

   ![](images/choose-document-type.png)

1. 选择 **[!UICONTROL 确定]** 关闭对话框。

1. 选择 **[!UICONTROL 下一个]**&#x200B;的

1. 在显示的窗口中，填写元数据部分中的所有必填字段，然后选择 **[!UICONTROL 保存]**&#x200B;的

   ![](images/metadata-details.png)

1. 它创建测试文档 **[!UICONTROL 草稿]** 状态，如下所示。

   ![](images/document-draft.png)

1. 在右上角，选择 ![齿轮图标](images/icon-gear.png) 下拉菜单并选择 **[!UICONTROL 开始审阅]**&#x200B;的

   ![](images/start-review.png)

1. 选择 **[!UICONTROL 审阅人]** 和 **[!UICONTROL 审阅截止日期]**&#x200B;的

1. 选择 **[!UICONTROL 开始]**&#x200B;的 它将文档状态更改为 [!UICONTROL 正在审阅中]的

   ![](images/in-review.png)

1. 代表审阅人完成所分配的任务。 完成后，它会将文档状态更改为 [!UICONTROL 已审阅]的

   ![](images/reviewed-status.png)

1. 选择 ![齿轮图标](images/icon-gear.png) 下拉菜单并选择 **[!UICONTROL Adobe Sign]**&#x200B;的

   ![](images/select-adobe-sign.png)

1. 在Vault中打开的iFrame窗口中，输入收件人的电子邮件地址并选择 **[!UICONTROL 下一个]**&#x200B;的

   ![](images/iframe.png)

   **注意：** 如果发送者的电子邮件不存在Adobe Sign用户帐户，则iFrame窗口会显示一条消息，如下所示。 它还会向用户发送一封电子邮件，其中包含激活帐户的说明。

   ![](images/iFrame-registration-message.png)

   ![](images/iFrame-confirm-email.png)

   但是，如果 *自动设置Sign用户* 功能已禁用，Adobe Sign用户创建失败，并且iFrame窗口显示一条消息，要求用户联系其Adobe Sign帐户管理员。 Adobe Sign帐户管理员可以采取以下任一操作：

   * 启用 *自动设置Sign用户* 功能。
   * 使用Veeva Vault Adobe Sign集成之前，在Adobe Sign中创建用户。

   ![](images/iFrame-contact-administrator.png)

1. 处理文档后，将签名字段从右侧面板拖放并选择 **[!UICONTROL 发送]**&#x200B;的

   ![](images/add-signature-fields.png)

1. 这会将文档发送给收件人以进行签名。 收件人收到文档电子邮件后，文档状态将从 [!UICONTROL 已审阅] 来 [!UICONTROL Adobe签名]的

   ![](images/in-adobe-signing.png)

1. 在Adobe Sign中捕获并完成所有签名后，文档Vault中的状态变为 [!UICONTROL 已批准]的

1. 选择 **[!UICONTROL 文档文件]** 选项并展开 **[!UICONTROL 演绎版]** 部分。 当文档处于“已批准”状态时，它会自动创建一个名为“Adobe Sign Rendition”的新格式副本。

   ![](images/document-files.png)

1. 下载Adobe Sign Rendition以验证收件人签名。

   ![](images/verify-signature.png)

## 使用Adobe Sign for [!DNL Veeva Vault] {#cancel-sign-vault-agreement}

1. 转到 [[!DNL Veeva Vault] 登录页](https://login.veevavault.com/) 然后输入您的用户名和密码。 这将打开Vault的主页，如下所示。

   ![](images/vault-home.png)

1. 选择 **[!UICONTROL 库]** 选项卡，然后选择文档。 文档状态可以是： [!UICONTROL 在Adobe Sign Draft中], [!UICONTROL 在Adobe Sign Authoring中]或 [!UICONTROL Adobe签名]的

   ![](images/document-adobe-sign-authoring.png)

1. 选择 **[!UICONTROL 取消Adobe Sign]**&#x200B;的

   ![](images/cancel-document.png)

1. 它触发Web操作并将iFrame窗口加载到 [!UICONTROL 保管库]的

   ![](images/cancelled-document.png)

1. 文档状态会自动更改为 [!UICONTROL 审阅]的

   ![](images/cancel-reviewed.png)

在文档状态更改为“审阅”后，您可以再次发送文档以请求签名。
