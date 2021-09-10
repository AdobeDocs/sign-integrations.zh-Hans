---
title: Workday 快速入门指南
description: 面向希望在Workday环境中使用Adobe Sign的客户的快速入门指南。
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: d462ccf41fa5483cfa02f5eaf154c23f26157a1e
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 37%

---

# [!DNL Workday] 快速入门指南{#workday-quick-start-guide}

[**联系 Adobe Sign 技术支持**](https://adobe.com/go/adobesign-support-center_cn)

## 概览 {#overview}

本文档旨在帮助[!DNL Workday]管理员了解如何自定义[!DNL Workday]业务流程以包括Adobe Sign以获取电子签名。 要在[!DNL Workday]中使用Adobe Sign，您必须知道如何创建和修改[!DNL Workday]项，例如：

* 业务流程框架
* 租户设置和配置
* 报告和[!DNL Workday] Studio集成

## 在 中访问 Adobe Sign[!DNL Workday] {#access-adobe-sign}

Adobe Sign电子签名功能在业务流程框架(BPF)中显示为[!UICONTROL 审阅文档步骤]操作，并显示为“分发文档”任务。

## [!UICONTROL 审阅文档步骤] {#review-document-step}

Adobe Sign for [!DNL Workday]通过[!UICONTROL 审阅文档步骤]公开，您可以将该步骤添加到[!DNL Workday]内的400多个业务流程中的任意一个，包括聘用、分发文档和任务、建议报酬等。

您可以参阅[!UICONTROL 审阅文档步骤]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)上的[[!DNL Workday] 社区文章。

[!UICONTROL [!UICONTROL 审阅文档步骤]s]与Adobe Sign的可开单事务之间存在1:1关系。 您可以在一个[!UICONTROL 审阅文档步骤]内合并多个文档，它们将作为单个包显示以供签名。

**注意**:在特定的 ** 审阅文档步骤中只能引 [!UICONTROL 用一个Dynamicdocument]。

要定义功能[!UICONTROL 审阅文档步骤]，请执行以下操作：

1. 插入[!UICONTROL 审阅文档步骤]。
1. 指定可以在[!UICONTROL 审阅文档步骤]上执行的组（角色）。

![业务流程步骤](images/insert-review-doc-steptornm-575.png)

配置[!UICONTROL 审阅文档步骤]:

1. 将&#x200B;*[!UICONTROL 电子签名集成类型]*&#x200B;指定为 *[!UICONTROL Adobe 提供的 eSign]*.

1. 在签名网格中添加行.

   * 签名网格指定文档被传递进行签名的序列顺序。每一行均包含一个或多个角色，并且每一行均代表签名流程中的一个步骤。
   * 特定步骤内角色的每一个成员都会收到通知：有一个签名事件处于待定状态.
   * 在角色中的一个人员签名后，行步骤即已完成并且文档将被移到下一个行步骤.
   * 当所有行都已签名后，[!UICONTROL 审阅文档步骤]将完成。

1. 指定要签名的文档。如果这是一个聘用业务流程，您可以使用“生成文档”步骤中的文档。否则，请选择一个现有的文档或报告。

1. 您可以根据需要对任意数量的文档重复步骤 3。

   ![配置审阅文档步骤](images/configure-rd-stepsmaller-575.png)

1. （可选）添加“重定向用户”以捕获“拒绝签名”操作。 当用户拒绝时，[!DNL Workday]将文档重新路由到配置的安全组进行审阅。

从[!UICONTROL 审阅文档步骤]的相关操作菜单中，选择&#x200B;**[!UICONTROL 业务流程]** > **[!UICONTROL 维护重定向]**。 接下来，选择以下选项之一：

* **[!UICONTROL 返回]**:使安全组成员能够向业务流程中的上一步骤发送一个步骤。业务流程将从该步骤重新启动。
* **[!UICONTROL 移至下一步]**:要使安全组成员能够将步骤转发到业务流程的下一步。
* **[!UICONTROL 安全组]**:重定向业务流程流程中的步骤。在“重定向”部分的业务流程安全性策略中，将选择在此提示中显示的安全组。

## 业务流程步骤说明 {#business-process-step-notes}

业务流程框架功能强大；但是，您必须确保：

* 每个业务流程都必须有一个完成步骤，这是业务流程结束时的理想选择。

* 完成步骤是在搜索图标的相关操作菜单中设置的。 这只有在“查看”业务流程时才可能，而在“编辑”业务流程时则不可能。

* 业务流程的每一个步骤都会按顺序执行.

   您可以通过更改顺序值来更改步骤的顺序。 例如，要在项目“c”和“d”之间插入一个步骤，请将新项目指定为“ca”。

### 示例：优惠 {#example-offer}

聘用业务流程是作业申请动态业务流程的一个子流程，需要配置该子流程以执行聘用业务流程。 当工作申请状态转为“聘用”或“招聘”时会触发此业务流程。

在下例中，[!UICONTROL 审阅文档步骤]在北美和日本都使用动态文档步骤。

![[!DNL Workday] 业务流程的示例](images/bp-for-offersmaller-575.png)

此业务流程执行以下操作：

* 要求BP的发起人建议对候选人的补偿（步骤b）。
* 使用步骤条件测试当前国家/地区是否不是日本。

   如果为true，则执行使用英语文档的步骤“ba”。

   如果为false，则执行使用日语文档的步骤“bb”。

* 在[!UICONTROL 审阅文档步骤] &quot;bc&quot;中定义签名过程。
* 定义要在所需完成步骤“d”中提供选件的决策点。

在步骤“ba”中生成的动态文档称为[!UICONTROL 聘用信]，并且包含一个名为[!UICONTROL 快速聘用]的文本块。您可以根据需要添加多个文本块，如页眉、问候语、报酬、股票、结束语、术语等。

![[!DNL Workday] 查看文档页面](images/offer-letter-575.png)

下面的动态聘用信是在[!DNL Workday]富文本编辑器中创建的。 *gray*&#x200B;中高亮显示的项是[!DNL Workday]提供的引用上下文数据的对象。

{{括号}} 中的项目是 [Adobe 文本标记](https://adobe.com/go/adobesign_text_tag_guide_cn)。

![动态表单示例](images/script.png)

在[!UICONTROL 审阅文档步骤]中，动态文档从上一步引用，并通过两个签名组定义顺序签名过程。

下面所示的行为将首先将动态生成的文档发送给招聘经理，然后将其发送给候选人。

![[!DNL Workday] 已定义签名组](images/configure-rd-stepsmaller-575.png)

### 示例：分发文档 {#example-distribute-documents}

在[!DNL Workday] 30中引入的“批量分发文档”或“任务”任务可用于将单个文档发送给由单个签名者组成的大型组(&lt;20K)。 它仅限于每个文档的单个签名。通过从搜索栏访问“[!UICONTROL 创建分发文档或任务]”操作来创建分发。

示例：将员工权益选择表发送给 Global Modern Services 的所有经理。如果需要，您可以进一步将其过滤给单个管理器。

您还可以访问&#x200B;**查看分发文档或任务**&#x200B;报告来跟踪分发进度。

![](images/create-distributedocumentsortasks.png)

### 示例：报告 {#example-reporting}

[!DNL Workday] 具有一个丰富的报告基础结构。要查看 Adobe Sign 流程的详细信息，请检查&#x200B;*审阅文档事件*&#x200B;的元素。

以下是一个简单的自定义报告，它可在所有业务流程间运行以查找 Adobe Sign 事务及其状态。

![[!DNL Workday] 自定义报告的示例](images/review-document-eventsmaller-575.png)

以下报告通过查看实施租户内的聘用、入职和提议补偿业务流程而生成。

您可以看到：

* 文档已发出进行签名
* 关联的业务流程步骤
* 等待签名的下一个人员

![[!DNL Workday]使用三个对象的 报告的示例](images/workday-reportsmaller-575.png)

## 已签名文档 {#signed-documents}

[!DNL Workday]签名周期禁止Adobe Sign发送所有电子邮件通知。 用户会收到其[!DNL Workday]收件箱中挂起操作的通知。

当文档由所有签名组签名后，已签名文档的副本将通过电子邮件分发给签名组的所有成员。

要抑制此行为，您可联系Adobe Sign成功经理或[Adobe Sign支持团队](https://adobe.com/go/adobesign-support-center)。

在[!DNL Workday]中，您可以访问完整进程记录中的已签名文档。 您可能会发现：

* 工作人员配置文件中的工作人员文档，以及
* 候选人配置文件中的候选文档（聘用信）。

下图显示了候选人Chris Foxx的签名聘用信。

![优惠 [!DNL Workday] 信示例](images/offer.png)

## 支持 {#support}

### [!DNL Workday] 支持 {#workday-support}

[!DNL Workday] 是集成所有者，如果您要咨询有关集成范围问题、功能请求或集成日常功能问题，请首先联系 Workday。

[!DNL Workday]社区有几篇关于如何排除集成故障和生成文档的好文章：

* [电子签名集成疑难解答](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [审阅文档步骤](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [动态文档生成](https://community.workday.com/node/176443)
* [聘用文档生成配置提示](https://community.workday.com/node/183242)

### Adobe Sign支持 {#adobe-sign-support}

Adobe Sign 是集成合作伙伴，如果集成获取签名失败或待定签名通知失败时，请联系 Adobe Sign。

Adobe Sign 客户应当联系各自的客户成功经理 (CSM) 以寻求支持。或者，可以致电 1-866-318-4100 联系 Adobe 技术支持，等待对方播送产品列表，然后输入 4，接着再输入 2（根据提示）。

* [将 Adobe 文本标记添加到文档](https://adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
