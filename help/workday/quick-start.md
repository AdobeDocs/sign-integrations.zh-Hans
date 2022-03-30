---
title: Workday 快速入门指南
description: 适用于希望在Workday环境中使用Adobe Sign的客户的快速入门指南。
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 30%

---

# [!DNL Workday] 快速入门指南{#workday-quick-start-guide}

[**联系 Adobe Sign 技术支持**](https://www.adobe.com/go/adobesign-support-center)

## 概览 {#overview}

本文档旨在帮助您 [!DNL Workday] 管理员了解如何自定义 [!DNL Workday] 业务流程包含Adobe Sign以获取电子签名。 要在 [!DNL Workday]，您必须知道如何创建和修改 [!DNL Workday] 例如：

* [!UICONTROL 业务流程框架]
* 租户设置和配置
* 报告和 [!DNL Workday] Studio集成

## 在 中访问 Adobe Sign[!DNL Workday] {#access-adobe-sign}

[!UICONTROL Adobe Sign电子签名功能] 显示为 [!UICONTROL 审阅文档步骤] 在 [!UICONTROL 业务流程框架(BPF)] 以及分发文档任务。

## [!UICONTROL 审阅文档步骤] {#review-document-step}

适用于 [!DNL Workday] 通过 [!UICONTROL 审阅文档步骤] 可以添加到 [!DNL Workday]，包括 [!UICONTROL 优惠], [!UICONTROL 分发文档和任务], [!UICONTROL 建议赔偿]、等等。

您可以参阅 [[!DNL Workday] 社区文章 [!UICONTROL 审阅文档步骤]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)的

这两者之间存在1:1的关系 [!UICONTROL [!UICONTROL 审阅文档步骤]s] 以及Adobe Sign的计费交易。 您可以将多个文档合并为一个 [!UICONTROL 审阅文档步骤] 它们将显示为单个包以供签名。

**注释**:仅一个 *动态* 文档可以在特定的 [!UICONTROL 审阅文档步骤]的

要定义功能，请执行以下操作 [!UICONTROL 审阅文档步骤]:

1. 插入 [!UICONTROL 审阅文档步骤]的
1. 指定可执行操作的组（角色） [!UICONTROL 审阅文档步骤]的

![业务流程步骤](images/insert-review-doc-steptornm-575.png)

要配置 [!UICONTROL 审阅文档步骤]:

1. 将&#x200B;*[!UICONTROL 电子签名集成类型]*&#x200B;指定为 *[!UICONTROL Adobe 提供的 eSign]*.

1. 在签名网格中添加行.

   * 签名网格指定文档被传递进行签名的序列顺序。每一行均包含一个或多个角色，并且每一行均代表签名流程中的一个步骤。
   * 特定步骤内角色的每一个成员都会收到通知：有一个签名事件处于待定状态.
   * 在角色中的一个人员签名后，行步骤即已完成并且文档将被移到下一个行步骤.
   * 当所有行都已签名后， [!UICONTROL 审阅文档步骤] 已完成。

1. 指定要签名的文档。如果文档是 [!UICONTROL 优惠BP]，您可以在“生成文档”步骤中使用它。 否则，请选择一个现有的文档或报告。

1. 您可以根据需要对任意数量的文档重复步骤 3。

   ![配置审阅文档步骤](images/configure-rd-stepsmaller-575.png)

1. （可选）添加“重定向用户”以捕获“拒绝签名”操作。 当用户拒绝时， [!DNL Workday] 将文档重新路由至已配置的安全组以供审阅。

从 [!UICONTROL 审阅文档步骤]，请选择 **[!UICONTROL 业务流程]** > **[!UICONTROL 保持重定向]**&#x200B;的 接下来，选择以下选项之一：

* **[!UICONTROL 退回]**:要启用安全组成员将步骤发回到业务流程的上一个步骤，请执行以下操作： 业务流程将从该步骤重新启动。
* **[!UICONTROL 转到下一步]**:使安全组成员能够前进到业务流程的下一步。
* **[!UICONTROL 安全组]**:重定向业务流程中的步骤。 可在“重定向”部分的业务流程安全策略中，选择在此提示下显示的安全组。

## 业务流程步骤说明 {#business-process-step-notes}

[!UICONTROL 业务流程框架] 功能强大；但是，您必须确保：

* 每个业务流程都必须有一个完成步骤，最好是在业务流程结束时。

* 完成步骤由搜索图标的相关操作菜单来设置。 只有在“查看”BP时，而不是“编辑”BP时，才有可能做到这一点。

* 业务流程的每一个步骤都会按顺序执行.

   您可以通过更改顺序值来更改步骤的顺序。 例如，要在项目“c”和“d”之间插入一个步骤，请将新项目指定为“ca”。

### 示例：优惠 {#example-offer}

聘用业务流程是 [!UICONTROL 作业申请动态BP] 必须配置为执行选件BP。 将“作业应用程序”状态移到“”时触发[!UICONTROL 优惠]&quot;或&quot;[!UICONTROL 提供优惠]“。

在以下示例中， [!UICONTROL 审阅文档步骤] 正在北美和日本使用动态文档步骤。

![[!DNL Workday] 业务流程的示例](images/bp-for-offersmaller-575.png)

此业务流程执行以下操作：

* 要求BP的发起者为候选者建议补偿（步骤b）。
* 使用步骤条件测试当前国家/地区是否不是日本。

   如果为true，则执行使用英语文档的步骤“ba”。

   如果为false，则执行使用日语文档的步骤“bb”。

* 在中定义签名过程 [!UICONTROL 审阅文档步骤] &quot;bc&quot;
* 在要求的完成步骤“d”中定义要约的决策点。

在步骤“ba”中生成的动态文档称为[!UICONTROL 聘用信]，并且包含一个名为[!UICONTROL 快速聘用]的文本块。您可以根据需要添加多个文本块，如标题、问候、薪酬、图库、结束语、条款等。

![[!DNL Workday] 查看文档页面](images/offer-letter-575.png)

以下动态聘用信是在 [!DNL Workday] 富文本编辑器。 高亮显示的项目 *灰色* 是 [!DNL Workday] 提供了引用上下文数据的对象。

{{括号}} 中的项目是 [Adobe 文本标记](https://adobe.com/go/adobesign_text_tag_guide_cn)。

![动态表单示例](images/script.png)

在 [!UICONTROL 审阅文档步骤]，动态文档引用自上一步骤，并通过两个签名组定义顺序签名流程。

下述行为会将动态生成的文档首先传送至“聘用经理”，然后传送至“候选人”。

![[!DNL Workday] 正在定义的签名组](images/configure-rd-stepsmaller-575.png)

### 示例：分发文档 {#example-distribute-documents}

引入 [!DNL Workday] 30，批量分发文档或任务任务可用于将单个文档发送给大量(&lt;20K)的个人签名者。 它仅限于每个文档的单个签名。通过访问“[!UICONTROL 创建分发文档或任务]”操作。

示例：将员工权益选择表发送给具有 [!UICONTROL 全球现代服务]的 如果需要，您可以进一步对单个经理进行筛选。

您还可以访问 **查看分发文档或任务** 报告，以跟踪分发的进度。

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

## 已签名的文档 {#signed-documents}

在 [!DNL Workday] 签名周期禁止所有由Adobe Sign发送的电子邮件通知。 用户将被告知其应用程序内的待处理操作 [!DNL Workday] 收件箱。

所有签名组对文档进行签名后，系统会通过电子邮件将签名文档的副本分发给签名组的所有成员。

要禁止此行为，您可以联系 [!UICONTROL Adobe Sign Success Manager] 或 [Adobe Sign支持团队](https://adobe.com/go/adobesign-support-center)的

在 [!DNL Workday]，您可以在完整流程记录中访问已签名的文档。 您可能会发现：

* 工作人员配置文件上的工作人员文档，以及
* 候选人配置文件上的候选人文档（聘用信）。

下图显示了候选人Chris Foxx的已签名录用通知书。

![示例 [!DNL Workday] 聘用信](images/offer.png)

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

Adobe Sign客户应联系其客户成功经理以获得支持。 或者， [!UICONTROL Adobe技术支持] 可通过电话联系：1-866-318-4100，等待产品列表，然后输入：4和2（根据提示）。

* [将 Adobe 文本标记添加到文档](https://www.adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
