---
title: Veva Vault用户指南
description: Veeva Vault客户指南，介绍如何使用Adobe Sign与Veeva集成
products: Adobe Sign
content-type: reference
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 39a43637-af3f-432e-a784-8f472aa86df5
source-git-commit: 63a34c2d77ba7a262670da624c86a3730de0fdc5
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 3%

---

# Adobe Sign for [!DNL Veeva Vault]:用户指南 {#veeva-vault-user-guide}

[**联系 Adobe Sign 技术支持**](https://adobe.com/go/adobesign-support-center_cn)

本文档旨在帮助[!DNL Veeva Vault]客户了解如何使用Adobe Sign进行[!DNL Veeva Vault]集成以发送协议。

## 概览 {#overview}

Adobe Sign与[!DNL Veeva Vault]的集成有助于为任何需要合法签名或可审核文档处理的文档获取签名或批准的过程。

发送文档进行签名的整个过程与发送电子邮件类似，因此对大多数用户来说很容易采用。

Adobe Sign与[!DNL Veeva Vault]的集成简化了文档和签名工作流程并加快了工作流程。 通过使用集成工作流，您可以：

* 节省用于蜗牛邮件、隔夜送达和传真的时间和资源。
* 从[!DNL Veeva Vault]发送合同进行电子签名或审批，访问实时合同历史记录，并查看保存的合同。
* 在整个组织中实时跟踪交易，并在查看、签署、取消或拒绝协议时获取更新。
* 使用 20 多种语言进行电子签名，并在全球 50 多个区域支持回传服务.
* 创建可重复使用的协议模板以发送选项。

## 使用[!DNL Veeva Vault]的Adobe Sign发送协议 {#send-sign-vault-agreement}

要使用Adobe Sign for Veeva发送协议，请执行以下操作：

1. 转到[[!DNL Veeva Vault] 登录页](https://login.veevavault.com/)并输入您的用户名和密码。 它会打开Vault的主页，如下所示。

   ![](images/vault-home.png)

1. 选择&#x200B;**[!UICONTROL 库]**&#x200B;选项卡，然后从右上角选择&#x200B;**[!UICONTROL 创建]**。

   ![](images/create-library.png)

1. 选择&#x200B;**[!UICONTROL 上载并继续]**。

1. 从本地驱动器上传任何文档。

1. 在出现的对话框中，选择&#x200B;**[!UICONTROL 类型]**&#x200B;作为&#x200B;*[!UICONTROL Clinical]*，然后选择&#x200B;**[!UICONTROL 子类型]**&#x200B;和&#x200B;**[!UICONTROL 分类]**（如果需要）。

   ![](images/choose-document-type.png)

1. 选择&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭对话框。

1. 选择&#x200B;**[!UICONTROL Next]**。

1. 在显示的窗口中，填写元数据部分中的所有必填字段，然后选择&#x200B;**[!UICONTROL 保存]**。

   ![](images/metadata-details.png)

1. 它创建处于&#x200B;**[!UICONTROL Draft]**&#x200B;状态的测试文档，如下所示。

   ![](images/document-draft.png)

1. 从右上角，选择![齿轮图标](images/icon-gear.png)下拉菜单，然后选择&#x200B;**[!UICONTROL 开始审阅]**。

   ![](images/start-review.png)

1. 选择&#x200B;**[!UICONTROL 审阅人]**&#x200B;和&#x200B;**[!UICONTROL 审阅截止日期]**。

1. 选择&#x200B;**[!UICONTROL 开始]**。 它将文档状态更改为[!UICONTROL IN REVIEW]。

   ![](images/in-review.png)

1. 代表审阅人完成分配的任务。 完成后，文档状态将更改为[!UICONTROL REVIEWED]。

   ![](images/reviewed-status.png)

1. 选择![齿轮图标](images/icon-gear.png)下拉菜单，然后选择&#x200B;**[!UICONTROL Adobe Sign]**。

   ![](images/select-adobe-sign.png)

1. 在Vault中打开的iFrame窗口中，输入收件人的电子邮件地址，然后选择&#x200B;**[!UICONTROL Next]**。

   ![](images/iframe.png)

1. 处理文档后，从右侧面板拖放“签名”字段，然后选择&#x200B;**[!UICONTROL 发送]**。

   ![](images/add-signature-fields.png)

1. 它将文档发送给收件人进行签名。 收件人收到文档电子邮件后，文档状态将从[!UICONTROL Reviewed]更改为[!UICONTROL In Adobe Signing]。

   ![](images/in-adobe-signing.png)

1. 在Adobe Sign中捕获并完成所有签名后，Vault中的文档状态将更改为[!UICONTROL Approved]。

1. 选择“**[!UICONTROL 文档文件]**”选项，并展开Vault中的&#x200B;**[!UICONTROL 格式副本]**&#x200B;部分。 文档处于“批准”状态后，它会自动创建一个名为“Adobe Sign再现”的新再现。

   ![](images/document-files.png)

1. 下载Adobe Sign Rendition以验证接收签名。

   ![](images/verify-signature.png)

## 使用[!DNL Veeva Vault]的Adobe Sign取消协议 {#cancel-sign-vault-agreement}

1. 转到[[!DNL Veeva Vault] 登录页](https://login.veevavault.com/)并输入您的用户名和密码。 它会打开Vault的主页，如下所示。

   ![](images/vault-home.png)

1. 选择&#x200B;**[!UICONTROL 库]**&#x200B;选项卡，然后选择文档。 文档状态可以是：[!UICONTROL 在Adobe Sign Draft]中，[!UICONTROL 在Adobe Sign Authoring]中，或[!UICONTROL 在Adobe签名]中。

   ![](images/document-adobe-sign-authoring.png)

1. 选择&#x200B;**[!UICONTROL 取消Adobe Sign]**。

   ![](images/cancel-document.png)

1. 它触发Web动作，并加载[!UICONTROL Vault]中的iFrame窗口。

   ![](images/cancelled-document.png)

1. 文档状态会自动更改为[!UICONTROL Review]。

   ![](images/cancel-reviewed.png)

文档状态更改为“审阅”后，您可以再次发送文档以请求签名。
