---
title: '[!DNL Veeva Vault] 安装指南'
description: 支持Adobe Sign与Veeva集成的安装指南
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: 3f826e88969562a69279a29dfdd98775ec01fd51
workflow-type: tm+mt
source-wordcount: '3061'
ht-degree: 2%

---

# [!DNL Veeva Vault] 安装指南{#veeva-installation-guide}

[**联系 Adobe Sign 技术支持**](https://adobe.com/go/adobesign-support-center_cn)

## 概览 {#overview}

本文档介绍如何将Adobe Sign与[!DNL Veeva Vault]平台建立集成。 [!DNL Veeva Vault] 是为生命科学构建的企业内容管理(ECM)平台。“保管库”是一个内容和数据存储库，通常用于管理法规文件、研究报告、授权申请、一般合同等。 一个企业可以有多个“金库”，必须单独维护。

完成集成的高级步骤包括：

* 在Adobe Sign中激活您的管理帐户（仅限新客户）
* 创建对象以跟踪Vault中协议生命周期的历史记录。
* 创建新的安全性配置文件。
* 在Adobe Sign中配置组以容纳[!DNL Veeva Vault]集成用户。
* 创建文档字段和格式副本。
* 配置Web操作并更新文档生命周期。
* 创建文档类型用户和用户角色设置。

>[!NOTE]
>
>Adobe Sign管理员必须在Adobe Sign中执行Adobe Sign设置步骤。

## 配置[!DNL Veeva Vault]

要配置[!DNL Veeva Vault]以与Adobe Sign集成，我们会创建一些对象，帮助跟踪Vault中协议生命周期的历史记录。 管理员必须创建以下对象：

* 签名
* 签名人
* 签名事件
* 进程锁定器

### 创建签名对象  {#create-signature-object}

创建签名对象以存储与协议相关的信息。 Signature对象是一个数据库，它包含以下特定字段下的信息：

**签名对象字段**

| 字段 | 标签 | 类型 | 说明 |
| --- | --- | ---| --- | 
| external_id__c | 协议 ID | 字符串(100) | 持有Adobe Sign的唯一协议ID |
| file_hash_c | 文件哈希 | 字符串(50) | 保存已发送到Adobe Sign的文件的md5小组 |
| name_v | 名称 | 字符串(128) | 保存协议名称 |
| sender__c | 发件人 | 对象（用户） | 保存对已创建协议的Vault用户的引用 |
| signature_status_c | 签名状态 | 字符串(75) | 在Adobe Sign中保持协议状态 |
| signature_type_c | 签名类型 | 字符串(20) | 在Adobe Sign（书面或ESIGN）中保存协议的签名类型 |
| start_date_c | 开始日期 | 日期时间 | 协议发送以请求签名的日期 |
| cancellation_date_c | 取消日期 | 日期时间 | 暂挂协议取消的日期。 |
| completion_date_c | 完成日期 | 日期时间 | 保留协议完成的日期。 |
| viewable_rendition_used_c | 已使用可查看的节目 | 布尔 | 指示是否已发送可查看的节目以供签名的标志。 （默认情况下为true） |

![签名对象详细信息的图像](images/signature-object-details.png)

### 创建签名者对象 {#create-signatory-object}

创建签名对象以存储与协议中的参与者相关的信息。 它包含以下特定字段下的信息：

**签名对象字段**

| 字段 | 标签 | 类型 | 说明 |
| --- | --- | ---| --- | 
| email_c | 电子邮件 | 字符串(120) | 持有Adobe Sign的唯一协议ID |
| external_id__c | 参与者ID | 字符串(80) | 暂挂Adobe Sign唯一参与者的标识符 |
| name_v | 名称 | 字符串(128) | 暂挂Adobe Sign参与者的姓名 |
| order_c | 顺序 | 号码 | 暂挂Adobe Sign协议参与者的订单编号 |
| role__c | 角色 | 字符串(30) | 保留Adobe Sign协议参与者的角色 |
| signature_c | 签名 | 对象（签名） | 保存对签名父记录的引用 |
| signature_status_c | 签名状态 | 字符串(100) | 暂挂Adobe Sign协议参与者的状态 |
| user__c | 用户 | 对象（用户） | 如果参与者是Vault用户，则保留对签名者用户记录的引用 |

![签名者详细信息的图像](images/signatory-object-details.png)

### 创建签名事件对象  {#create-signature-event}

创建签名事件对象以存储协议的事件相关信息。 它包含以下特定字段下的信息：

| 字段 | 标签 | 类型 | 说明 |
| --- | --- | ---| --- | 
| acting_user_email_c | 代理用户电子邮件 | 字符串 | 保存执行导致生成事件的操作的Adobe Sign用户的电子邮件 |
| acting_user_name__c | 代理用户名 | 字符串 | 保存执行导致生成事件的操作的Adobe Sign用户的名称 |
| description_c | 说明 | 字符串 | 保存Adobe Sign事件的说明 |
| event_date_c | 事件日期 | 日期时间 | 保存Adobe Sign事件的日期和时间 |
| event_type_c | 事件类型 | 字符串 | 保存Adobe Sign事件的类型 |
| name_v | 名称 | 字符串 | 自动生成的事件名称 |
| participant_comment__c | 参与者注释 | 字符串 | 保留Adobe Sign参与者的注释（如果有） |
| participant_email__c | 参与者电子邮件 | 字符串 | 保存Adobe Sign参与者的电子邮件 |
| participant_role__c | 参与人角色 | 字符串 | 担任Adobe Sign参与者的角色 |
| signature_c | 签名 | 对象（签名） | 保存对签名父记录的引用 |

![签名事件详细信息的图像](images/signature-event-object-details.png)

### 创建Process Locker对象  {#create-process-locker}

将创建一个Process Locker对象以锁定Adobe Sign集成进程。 它不需要任何自定义字段。

![签名事件详细信息的图像](images/process-locker-details.png)

## 创建安全性配置文件{#security-profiles}

为了成功集成Vault，将创建一个名为&#x200B;*Adobe Sign集成配置文件*&#x200B;的新安全配置文件，并为&#x200B;*Adobe Sign管理操作*&#x200B;设置其权限。 Adobe Sign集成配置文件被分配给系统帐户，并由集成在调用Vault API时使用。 此配置允许以下用户具有以下权限：

* 保管库API
* 读取、创建、编辑和删除：签名、签名者、签名事件和流程更衣器对象

![签名事件详细信息的图像](images/security-profiles.png)

需要访问Vault中Adobe Sign历史记录的所有用户的安全配置文件都必须具有“签名读取”、“签名者”和“签名事件”对象的权限。

![签名事件详细信息的图像](images/set-permissions.png)

## 创建组 {#create-group}

要为[!DNL Vault]配置Adobe Sign，将创建一个名为&#x200B;*Adobe Sign管理组*&#x200B;的新组。 此组用于设置Adobe Sign相关字段的文档字段级别安全性，默认情况下应包括&#x200B;*Adobe Sign集成配置文件*。

![签名事件详细信息的图像](images/create-admin-group.png)

## 创建用户 {#create-user}

Adobe Sign集成的Vault系统帐户用户必须：

* 具有Adobe Sign集成配置文件
* 具有安全性配置文件
* 具有禁用密码过期的特定安全策略
* 成为Adobe Sign Admin Group的成员。

要确保系统帐户用户在特定文档生命周期中属于Adobe Sign管理组，您必须创建用户角色设置记录。

## 创建应用程序角色 {#create-application-roles}

必须创建名为&#x200B;*Adobe Sign Admin Role*&#x200B;的应用程序角色。 此角色必须在符合Adobe签名条件的每种文档类型的生命周期中定义。 对于Adobe Sign的每个特定生命周期状态，都会添加Adobe Sign管理员角色并使用相应的权限进行配置。

![创建应用程序角色的映像](images/create-application-roles.png)

## 创建文档域 {#create-fields}

要与Adobe Sign建立集成，管理员必须创建以下两个新的共享文档字段：

* 签名(signature__c)
* 允许Adobe Sign用户操作(allow_adobe_sign_user_actions__c)

![文档详细信息的图像](images/create-document-fields.png)

这些共享字段必须添加到符合Adobe签名条件的所有文档类型。 这两个字段都应具有特定的安全性，该安全性仅允许Adobe Sign管理组成员更新其值。

![签名字段详细信息的图像](images/signature-field-details.png)

管理员必须添加现有共享字段&#x200B;*禁用保管库叠加(disable_vault_overlays_v)*，并对于所有符合Adobe签名条件的文档类型将其设置为活动。 （可选）该字段可以具有特定的安全性，该安全性仅允许Adobe Sign管理员组的成员更新其值。

![允许adobe sign用户操作的图像](images/allow-adobe-sign-user-actions.png)

## 创建文档格式副本 {#create-renditions}

管理员必须创建名为&#x200B;*Adobe Sign Rendition(adobe_sign_rendition__c)*&#x200B;的新格式副本类型，Vault集成使用该类型将签名的PDF文档上载到Adobe Sign。 应为符合Adobe Sign签名条件的每种文档类型声明Adobe格式副本。

![再现类型的图像](images/rendition-type.png)

![再现类型的图像](images/edit-details-clinical-type.png)

## 配置Web动作 {#web-actions}

Adobe Sign和保管库集成要求您创建和配置以下两个Web操作：

* **创建Adobe Sign**:它创建或显示Adobe Sign协议。

   类型：文档
目标：在Vault中显示
URL:<https://{integrationDomain}/adobe-sign-int/signature?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&sessionId=${Session.id}&vaultId=${Vault.Id>

* **取消Adobe Sign**:它取消Adobe Sign中的现有协议，并将文档的状态还原为初始状态。

   类型：文档
目标：在Vault中显示
URL:<https://{integrationDomain}/adobe-sign-int/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&sessionId=${Session.id}&vaultId=${Vault.Id>

## 更新文档生命周期 {#document-lifecycle}

对于符合Adobe签名条件的每种文档类型，必须通过添加新的生命周期角色和状态来更新相应的文档生命周期。

### 生命周期角色 {#lifecycle-role}

Adobe Sign管理应用程序角色必须添加到符合Adobe签名资格的文档使用的所有生命周期中。 应使用以下选项创建此角色：

* 启用动态访问控制
* 仅包含文档类型组的文档共享规则

![生命周期管理员角色的映像](images/document-lifecycle-admin-role.png)

### 生命周期状态 {#lifecycle-states}

Adobe Sign协议生命周期具有以下状态：

* 草稿
* 创作或DOCUMENTS_NOT_YTER_PROCESSED
* OUT_FOR_SIGNATURE或OUT_FOR_APPROVAL
* 已签名或已批准
* 已取消
* 已过期

将Vault文档发送到Adobe Sign时，其状态应与协议所在的状态相对应。 通过在有资格进行Adobe签名的文档使用的每个生命周期中添加以下状态来完成此操作：

* **Adobe签名前** （已审阅）：这是一个占位符名称，用于表示文档可从中发送到Adobe Sign的状态。根据文档类型，它可以是“草稿”状态或“已审阅”。 可以根据客户的要求自定义文档状态标签。 在Adobe签名状态之前，必须定义以下两个用户操作：

   * 将文档状态更改为&#x200B;*在Adobe Sign Draft*&#x200B;状态的操作。 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将Web操作称为“Adobe Sign”的操作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑域、编辑关系、下载源、管理可查看的节目和更改状态。

   ![生命周期状态1的映像](images/lifecycle-state1.png)

* **在Adobe Sign草稿中**:这是状态的占位符名称，指示文档已上载到Adobe Sign且其协议处于DRAFT状态。这是必需状态。 此状态必须遵循以下五个用户操作：

   * 将文档状态更改为&#x200B;*在Adobe Sign编辑中*&#x200B;状态的操作。 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将文档状态更改为&#x200B;*处于Adobe签名状态*&#x200B;的操作。 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将文档状态更改为&#x200B;*Adobe Sign Cancelled*&#x200B;状态的操作。 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将Web操作称为“Adobe Sign”的操作。
   * 调用Web动作“取消Adobe Sign”的动作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑域、编辑关系、下载源、管理可查看的节目和更改状态。

   ![生命周期状态2的映像](images/lifecycle-state2.png)

* **在Adobe Sign编辑中**:这是状态的占位符名称，指示文档已上载到Adobe Sign，且其协议处于“编辑”或“DOCUMENTS_NOT_YET_PROCESSED”状态。这是必需状态。 此状态必须定义以下四个用户操作：

   * 将文档状态更改为“Adobe Sign已取消”状态的操作。 无论生命周期是什么，所有文档类型的此用户操作的名称都必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将文档状态更改为“正在Adobe签名”状态的操作。 无论生命周期是什么，所有文档类型的此用户操作的名称都必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将Web操作称为“Adobe Sign”的操作
   * 调用Web动作“取消Adobe Sign”的动作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑域、编辑关系、下载源、管理可查看的节目和更改状态。

   ![生命周期状态3的映像](images/lifecycle-state3.png)

* **在Adobe签名中**:这是状态的占位符名称，指示文档已上载到Adobe Sign且其协议已发送给参与者（OUT_FOR_SIGNATURE或OUT_FOR_APPROVAL状态）。这是必需状态。 此状态必须定义以下五个用户操作：

   * 将文档状态更改为“Adobe Sign已取消”状态的操作。 此操作的目标状态可以是任何客户要求，也可以是不同类型的不同状态。 无论生命周期是什么，所有文档类型的此用户操作的名称都必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将文档状态更改为“Adobe Sign拒绝”状态的操作。 此操作的目标状态可以是任何客户要求，也可以是不同类型的不同状态。 无论生命周期是什么，所有文档类型的此用户操作的名称都必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 将文档状态更改为“Adobe签名”状态的操作。 此操作的目标状态可以是任何客户要求，也可以是不同类型的不同状态。 但是，无论生命周期是什么，所有用户操作的名称都必须相同。 如果需要，此操作的条件可设置为“允许Adobe Sign用户操作等于是”。
   * 调用Web操作&#x200B;*Adobe Sign*&#x200B;的操作。
   * 调用Web操作&#x200B;*取消Adobe Sign*&#x200B;的操作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑域、编辑关系、下载源、管理可查看的节目和更改状态。

   ![生命周期状态4的映像](images/lifecycle-state4.png)

* **Adobe已签名（已批准）**:这是状态的占位符名称，指示文档已上载到Adobe Sign且其协议已完成（“已签名”或“已批准”状态）。它是必需状态，可以是现有的生命周期状态，如“已批准”。
此状态不需要用户操作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容和编辑域。

下图演示了Adobe Sign协议和Vault文档状态之间的映射，其中“Adobe签名前”状态为“草稿”。

![Adobe Sign Vault映射的图像](images/sign-vault-mappings.png)

## 创建文档类型组和用户角色设置  {#document-type-group-user-role}

### 创建文档类型组 {#create-document-type-group}

管理员必须创建名为“Adobe Sign文档”的新文档类型组记录。 此文档类型组将添加到符合Adobe Sign流程条件的所有文档分类中。 由于文档类型组属性不是从类型继承到子类型，也不是从子类型继承到分类级别，因此必须为每个符合Adobe Sign条件的文档分类设置该属性。

![文档类型的图像](images/document-type.png)

### 创建用户角色设置 {#create-user-role-setup}

在正确配置生命周期后，系统应确保Adobe Sign Admin用户由DAC添加到所有符合Adobe Sign进程条件的文档。 通过创建相应的用户角色设置记录来完成此操作，该记录指定：

* 文档类型组为“Adobe Sign文档”，
* 应用程序角色为“Adobe Sign管理员角色”，
* 集成用户。

![用户角色设置的图像](images/user-role-setup.png)

>[!NOTE]
>
>如果用户角色设置对象不包含引用文档类型组对象的字段，则应添加此字段。

## 使用中间件将[!DNL Veeva Vault]连接到Adobe Sign {#connect-middleware}

Adobe Sign帐户管理员必须按照以下步骤使用中间件将[!DNL Veeva Vault]连接到Adobe Sign:

1. [转到Adobe Sign  [!DNL Veeva Vault] forHome页](https://static.adobesigncdn.com/veevavaultintsvc/index.html)。
1. 从右上角选择&#x200B;**[!UICONTROL 登录]**。

   ![中间件登录映像](images/middleware_login.png)

1. 在打开的Adobe Sign登录页中，提供帐户管理员电子邮件和密码，然后选择&#x200B;**[!UICONTROL 在]**&#x200B;中使用。

   ![图像](images/middleware-signin.png)

   用户登录后，页面右上角会显示关联的电子邮件ID和其他“设置”选项卡，如下所示。

   ![图像](images/middleware_settings.png)

1. 选择&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡。

   “设置”页面显示可用的连接，在首次设置连接时不显示任何连接，如下所示。

   ![图像](images/middleware_newconnection.png)

1. 选择&#x200B;**[!UICONTROL 添加连接]**&#x200B;以添加新连接。

1. 在打开的“添加连接”对话框中，提供所需的详细信息，包括[!DNL Veeva Vault]凭据。

   Adobe Sign凭据会从初始Adobe Sign登录中自动填充。

   ![图像](images/middleware_addconnection.png)

1. 选择&#x200B;**[!UICONTROL 验证]**&#x200B;以验证帐户详细信息。

   成功验证后，您会看到“用户验证成功”通知，如下所示。

   ![图像](images/middleware_validated.png)

1. 要限制对特定Adobe Sign组的使用，请展开&#x200B;**[!UICONTROL 组]**&#x200B;下拉列表，然后选择可用组之一。

   ![图像](images/middleware_group.png)

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存新连接。

   新连接显示在“设置”选项卡下，显示[!DNL Veeva Vault]和Adobe Sign之间的成功集成。

   ![图像](images/middleware_setup.png)

## 包部署生命周期 {#deployment-lifecycle}

### 一般部署生命周期 {#general-deployment}

**步骤 1.** 创建一个名为“Adobe Sign管理员角色”的新应用程序角色。

**步骤 2.** 创建一个名为“Adobe Sign文档”的新文档类型组。

**步骤 3.** 部署包。

**步骤4.** 新建一个名为“Adobe Sign管理组”的用户管理组。

**步骤5.** 使用安全配置文件“Adobe Sign集成配置文件”创建集成用户配置文件，并将其分配给Adobe Sign管理组。

**步骤6.** 为需要访问Vault中Adobe Sign历史记录的用户将所有安全配置文件的读者权限分配给“签名”、“签名”和“签名事件”对象。

**第7步。** 在符合Adobe Sign签名资格的每种文档类型的生命周期中定义Admin Role。对于每个Adobe Sign特定的生命周期状态，将添加此角色并使用相应的权限进行配置。

**第8步。** 为符合Adobe Sign签名条件的每种文档类型声明Adobe Rendition。

**第9步。** 对于符合Adobe签名条件的每种文档类型，通过添加新的生命周期角色和状态来更新相应的文档生命周期。

**第10步。** 为所有符合Adobe Sign流程条件的文档分类添加名为“Adobe Sign文档”的文档类型组。

**第11步。** 完成所有配置后，系统应确保Adobe Sign Admin用户由DAC添加，以用于所有符合Adobe Sign进程条件的文档。为此，请创建相应的用户角色设置记录，将文档类型组指定为“Adobe Sign文档”，将应用程序角色指定为“Adobe Sign管理员角色”和集成用户。

### 特定部署生命周期 {#specific-deployment}

**步骤 1.** 创建一个名为“Adobe Sign管理员角色”的新应用程序角色。

**步骤 2.** 新建一个名为“Adobe Sign文档”的文档类型组。

**步骤 3.** 部署包。

**步骤4.** 新建一个名为“Adobe Sign管理组”的用户管理组。

**步骤5.** 使用名为“Adobe Sign集成配置文件”的安全配置文件创建一个集成用户配置文件，并分配给Adobe Sign管理员组。
