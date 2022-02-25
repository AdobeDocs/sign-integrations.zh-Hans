---
title: '"[!DNL Veeva Vault] 安装指南"'
description: 启用Adobe Sign与Veeva集成的安装指南
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: 04a3e58da81c1a034318807776077d0076eec85f
workflow-type: tm+mt
source-wordcount: '3431'
ht-degree: 3%

---

# [!DNL Veeva Vault] 安装指南{#veeva-installation-guide}

[**联系 Adobe Sign 技术支持**](https://adobe.com/go/adobesign-support-center_cn)

## 概览 {#overview}

本文档介绍如何将Adobe Sign与 [!DNL Veeva Vault] 平台。 [!DNL Veeva Vault] 是一个为生命科学而构建的企业内容管理(ECM)平台。 “存储库”是一个内容和数据存储库，通常用于法规归档、研究报告、授权应用程序、总承包等。 单个企业可以有多个必须单独维护的“保管库”。

完成集成的高级步骤包括：

* 在Adobe Sign中激活您的管理帐户（仅限新客户）。
* 在Vault中创建对象以跟踪协议生命周期的历史记录。
* 创建新的安全性配置文件。
* 在Adobe Sign中配置组以容纳 [!DNL Veeva Vault] 集成用户。
* 创建文档字段和演绎版。
* 配置Web操作并更新文档生命周期。
* 创建文档类型用户和用户角色设置。
* 使用中间件将Veeva Vault连接到Adobe Sign。

>[!NOTE]
>
>Adobe Sign管理员必须在Adobe Sign中执行Adobe Sign设置步骤。

## 配置 [!DNL Veeva Vault] {#configure-veeva}

要配置 [!DNL Veeva Vault] 要与Adobe Sign集成，您需要实施下面列出的步骤。

### 步骤 1. 创建组 {#create-group}

要为 [!DNL Vault]，一个新组名为 *Adobe Sign Admin Group* 的条目。 此组用于为Adobe Sign相关字段设置文档字段级别安全性，并应包括 *Adobe Sign集成配置文件* 默认情况下。

![签名事件详细信息的图像](images/create-admin-group.png)

### 步骤 2. 部署包 {#deploy-package}

[部署包](https://helpx.adobe.com/content/dam/help/en/PKG-AdobeSign-Integration.zip) 然后按照步骤操作。 部署后，程序包将创建：

* 自定义对象：签名对象、签名者对象、签名事件对象、处理保险箱对象
* 签名对象页面布局
* 签名事件对象页面布局
* 签名者对象页面布局
* Process Locker对象页面布局
* Adobe Sign Rendition type
* 共享字段__c , allow_adobe_sign_user_actions__c
* Adobe Sign Web操作
* 取消Adobe Sign Web操作
* Adobe Sign管理员操作权限集
* Adobe Sign Integration Profile安全配置文件
* 应用程序角色Adobe Sign管理员角色
* 文档类型组“Adobe Sign Document”

#### 签名对象 {#signature-object}

创建签名对象以存储与协议相关的信息。 签名对象是一个数据库，它包含以下特定字段下的信息：

**签名对象字段**

| 字段 | 标签 | 类型 | 说明 |
| --- | --- | ---| --- | 
| external_id__c | 协议 ID | 字符串(100) | 保留Adobe Sign的唯一协议ID |
| file_hash__c | 文件哈希 | 字符串(50) | 保存已发送到Adobe Sign的文件的md5校验和 |
| name__v | 名称 | 字符串(128) | 保留协议名称 |
| sender__c | 发件人 | 对象（用户） | 保留对创建协议的存储库用户的引用 |
| signature_status__c | 签名状态 | 字符串(75) | 保留协议在Adobe Sign中的状态 |
| signature_type__c | 签名类型 | 字符串(20) | 在Adobe Sign（书面或ESIGN）中保留协议的签名类型 |
| start_date__c | 开始日期 | 日期时间 | 发送协议以请求签名的日期 |
| cancellation_date__c | 取消日期 | 日期时间 | 保留取消协议的日期。 |
| completion_date__c | 完成日期 | 日期时间 | 保留协议完成的日期。 |
| viewable_rendition_used__c | 已使用可查看的呈现形式 | 布尔 | 指示是否已发送可查看的呈现形式以进行签名的标记。 （默认情况下为true） |

![签名对象详细信息的图像](images/signature-object-details.png)

#### 签署人对象 {#signatory-object}

创建签名者对象以存储与协议中的参与者相关的信息。 它包含以下特定字段下的信息：

**签名者对象字段**

| 字段 | 标签 | 类型 | 说明 |
| --- | --- | ---| --- | 
| email__c | 电子邮箱 | 字符串(120) | 保留Adobe Sign的唯一协议ID |
| external_id__c | 参与者Id | 字符串(80) | 保留Adobe Sign唯一参与者的标识符 |
| name__v | 名称 | 字符串(128) | 包含Adobe Sign参与者的姓名 |
| order__c | 顺序 | 数字 | 保留Adobe Sign协议参与人的订单编号 |
| role__c | 角色 | 字符串(30) | 持有Adobe Sign协议参与者的角色 |
| signature__c | 签名 | 对象（签名） | 保留对签名父记录的引用 |
| signature_status__c | 签名状态 | 字符串(100) | 保留Adobe Sign协议参与人的状态 |
| user__c | 用户 | 对象（用户） | 如果参与者是保管库用户，则保存对签名人用户记录的引用 |

![签名者详细信息的图像](images/signatory-object-details.png)

#### 签名事件对象 {#signature-event}

创建签名事件对象是为了存储与协议事件相关的信息。 它包含以下特定字段下的信息：

| 字段 | 标签 | 类型 | 说明 |
| --- | --- | ---| --- | 
| acting_user_email__c | 代理用户电子邮件 | 字符串 | 保留执行导致生成事件的操作的Adobe Sign用户的电子邮件 |
| acting_user_name__c | 代理用户名 | 字符串 | 保留执行导致生成事件的操作的Adobe Sign用户的名称 |
| description__c | 说明 | 字符串 | 包含Adobe Sign事件的描述 |
| event_date__c | 事件日期 | 日期时间 | 保存Adobe Sign事件的日期和时间 |
| event_type__c | 事件类型 | 字符串 | 保留Adobe Sign事件的类型 |
| name__v | 名称 | 字符串 | 自动生成的事件名称 |
| participant_comment__c | 参与者注释 | 字符串 | 包含Adobe Sign参与人的注释（如果有） |
| participant_email__c | 参与者电子邮件 | 字符串 | 保留Adobe Sign参与人的电子邮件 |
| participant_role__c | 参与人角色 | 字符串 | 具有Adobe Sign参与者的角色 |
| signature__c | 签名 | 对象（签名） | 保留对签名父记录的引用 |

![图像](images/signature-event-object-details.png)

#### Process Locker对象 {#process-locker}

将创建进程锁存器对象以锁定Adobe Sign集成进程。 它不需要任何自定义字段。

![签名事件详细信息的图像](images/process-locker-details.png)

作为部署包的一部分提供的“签名”、“签名事件”、“签名事件”和“处理保险箱”对象默认启用“此对象的审核数据更改”属性。

**注意：** 通过启用“审核数据更改”设置，可以使Vault捕获对象在审核日志中记录数据更改。 默认情况下，此设置处于关闭状态。 启用此设置并创建记录后，便无法再禁用它。 如果关闭此设置且记录存在，则只有Vault所有者才能更新设置。

#### **显示签名对象的参与者和历史记录** {#display-participants-history}

作为部署包的一部分提供的“签名”对象随 [签名详细信息页面布局](https://vvtechpartner-adobe-rim.veevavault.com/ui/#admin/content_setup/object_schema/pagelayout?t=signature__c&amp;d=signature_detail_page_layout__c)的 “页面布局”中包含“参与者”和“历史记录”部分。

* 在 *参与者* 章节的“相关对象”部分已如下图所示进行配置。

   ![图像](images/edit-related-objects.png)

* 您可以编辑将为参与者显示的列，如下所示。

   ![图像](images/set-columns-to-display.png)

* 在 *历史记录* 章节的“相关对象”部分已如下图所示进行配置。

   ![图像](images/edit-related-object-in-history.png)

* 您可以编辑为“历史记录”显示的列，如下所示。

   ![图像](images/select-columns-to-display.png)

#### **查看Adobe Sign文档的参与者和审核历史记录** {#view-participants-audit-history}

* 要查看Adobe Sign文档的参与者和审核历史记录，请选择文档“Adobe签名”部分中的链接。

   ![图像](images/view-participants-audit-history.png)

* 打开的页面将显示Adobe Sign文档的参与者和历史记录，如下所示。

   ![图像](images/participants-and-history.png)

* 查看签名的审核记录，如下所示。

   ![图像](images/audit-trail.png)

### 步骤 3. 设置安全性配置文件 {#security-profiles}

在步骤2中成功部署包将创建Adobe Sign集成配置文件。 Adobe Sign集成配置文件被分配给系统帐户，并由集成在调用Vault API时使用。 此配置文件允许具有以下权限：

* Vault API
* 阅读、创建、编辑和删除：签名、签名者、签名事件和处理保险箱对象

您必须通过将包含的安全配置文件设置为Adobe Sign集成配置文件来更新Adobe Sign管理员组（在步骤1中创建），如下图所示。

![签名事件详细信息的图像](images/security-profiles.png)

### 步骤 4. 创建用户 {#create-user}

Adobe Sign集成的Vault系统帐户用户必须：

* 拥有Adobe Sign集成配置文件
* 拥有安全配置文件
* 具有禁用密码过期的特定安全策略
* 成为Adobe Sign Admin Group的成员。

为此，请执行以下步骤：

1. 创建Adobe Sign集成的Vault系统帐户用户。

   ![签名事件详细信息的图像](images/create-user.png)

2. 将用户添加到Adobe Sign Admin Group。

   ![签名事件详细信息的图像](images/add-user.png)

### 步骤 5. 配置文档类型组 {#create-document-type-group}

部署Adobe Sign包时，它会创建名为“Adobe Sign文档”的文档类型组记录。

![文档类型组的图像](images/document-type-groups.png)

您需要为适用于Adobe Sign流程的所有文档分类添加此文档类型组。 由于文档类型组属性既不是从类型继承到子类型，也不是从子类型继承到分类级别，因此必须为符合Adobe Sign条件的每个文档分类设置该属性。

![文档编辑详细信息的图像](images/document-edit-details.png)

**注意：** 如果用户角色设置对象不包含引用文档类型组对象的字段，则必须添加该字段。 为此，请转到 **[!UICONTROL 对象]** > **[!UICONTROL 用户角色设置]** > **[!UICONTROL 字段]** 并完成所需的步骤，如下图所示。

![用户角色设置的图像](images/create-setup-field.png)

![文档类型的图像](images/document-type.png)

### 步骤 6. 创建用户角色设置 {#create-user-role-setup}

正确配置生命周期后，系统应确保DAC为适用于Adobe Sign进程的所有文档添加Adobe Sign管理员用户。 为此，请创建相应的用户角色设置记录，其中指定：

* 文档类型组作为Adobe Sign文档
* 作为Adobe Sign管理员角色的应用程序角色
* 集成用户

![用户角色设置的图像](images/user-role-setup.png)

### 步骤 7. 设置文档字段 {#create-fields}

包部署将创建以下两个新的共享文档字段，它们对于建立集成是必需的：

* 签名(签名__c)
* 允许Adobe Sign用户操作(allow_adobe_sign_user_actions__c)

![图像](images/2-document-fields.png)

要设置文档字段，请执行以下操作：

1. 转到“配置”选项卡并选择 **[!UICONTROL 文档字段]** > **[!UICONTROL 共享字段]**&#x200B;的
1. 在“显示区段”字段中，选择 **[!UICONTROL 创建显示部分]** 和分配 **[!UICONTROL Adobe签名]** 作为章节标签。

   ![图像](images/create-display-section.png)

1. 对于两个共享文档字段(signature__c和allow_adobe_sign_user_actions__c)，请使用以下内容更新UI部分： **[!UICONTROL Adobe签名]** 作为章节标签。
1. 将这三个共享字段添加到所有符合文档签名条件的Adobe类型。 为此，请在“基本文档”页面中选择 **[!UICONTROL 添加]** > **[!UICONTROL 现有共享字段]** 右上角。

   ![图像](images/create-document-fields.png)

   ![图像](images/add-existing-fields.png)

   ![图像](images/use-shared-fields.png)

1. 请注意，这两个字段必须具有仅允许Adobe Sign管理员组成员更新其值的特定安全性。

   ![图像](images/security-overrides.png)

“禁用电子仓库叠加”(disable_vault_overlays__v)是现有的共享字段。 或者，该字段可以具有特定的安全性，该安全性仅允许Adobe Sign管理员组的成员更新其值。

### 步骤 8. 声明文档演绎版 {#declare-renditions}

新的格式副本类型称为 *Adobe Sign Rendition(adobe_sign_rendition__c)* 由Vault集成用于将已签名的PDF文档上传到Adobe Sign。 您必须为每个文档类型声明Adobe Sign格式副本，才有资格进行Adobe签名。

![呈现类型的图像](images/rendition-type.png)

![呈现类型的图像](images/edit-details-clinical-type.png)

### 步骤 9. 更新Web操作 {#web-actions}

Adobe Sign和Vault集成要求您创建和配置以下两个Web操作：

* **创建Adobe Sign**:它会创建或显示Adobe Sign协议。

   类型：文档目标：在保管库凭据中显示：通过发布消息URL启用发布会话凭据： <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![创建Adobe Sign的图像](images/create-adobe-sign.png)

* **取消Adobe Sign**:这会取消Adobe Sign中的现有协议，并将文档状态恢复为初始协议。

   类型：文档目标：在保管库凭据中显示：通过发布消息URL启用发布会话凭据：: <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![取消Adobe Sign的图像](images/cancel-adobe-sign.png)

### 步骤 10. 更新文档生命周期 {#document-lifecycle}

对于符合“Adobe签名”条件的每个文档类型，您都必须通过添加新生命周期角色和状态来更新相应的文档生命周期。

Adobe Sign协议生命周期包括以下状态：

* 草稿
* AUTHORING或DOCUMENTS_NOT_YET_PROCESSED
* OUT_FOR_SIGNATURE或OUT_FOR_APPROVAL
* 已签名或已批准
* 已取消
* 已过期

要更新文档生命周期，请执行以下步骤：

1. 添加生命周期角色。 必须将Adobe Sign管理员应用程序角色添加到有资格进行Adobe签名的文档使用的所有生命周期中，如下所示。

   ![生命周期管理角色图像](images/document-lifecycle-admin-role.png)

   应使用以下选项创建管理员角色：

   * 已启用动态访问控制。
   * 仅包括文档类型组的文档共享规则，如下图所示。

   ![Adobe Sign共享规则的图像](images/adobe-sign-sharing-rule.png)

2. 创建生命周期状态。 为此，请转到 **[!UICONTROL 设置]** > **[!UICONTROL 配置]** > **[!UICONTROL 文档生命周期]** > **[!UICONTROL 一般生命周期]** > **[!UICONTROL 状态]** > **[!UICONTROL 创建]**&#x200B;的 接下来，创建以下状态：

   * 在Adobe Sign Draft中

   ![Adobe Sign共享规则的图像](images/create-draft-state.png)

   * 在Adobe Sign Authoring中

   ![Adobe Sign共享规则的图像](images/create-authoring-state.png)

   * Adobe签名

   ![Adobe Sign共享规则的图像](images/create-signing-state.png)

3. 将用户操作添加到以下列出的状态。

   将Vault文档发送到Adobe Sign时，其状态应对应于协议所处的状态。 为此，请在符合“Adobe签名”条件的文档所使用的每个生命周期中添加以下状态：

   * **进行Adobe签名** （审阅）：这是文档可以从中发送到Adobe Sign的状态的占位符名称。 根据文档类型，可以将其设为“草稿”状态或“审阅”。 可以根据客户要求自定义文档状态标签。 在“Adobe签名”状态之前，必须定义以下两个用户操作：

      * 将文档状态更改为 *在Adobe Sign Draft中* 状态。 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 调用Web操作“Adobe Sign”的操作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑字段、编辑关系、下载源、管理可查看的呈现形式以及更改状态。

      ![生命周期状态1的图像](images/lifecycle-state1.png)

   * **在Adobe Sign Draft中**:这是一个占位符名称，表示文档已上载至Adobe Sign，且其协议处于“草稿”状态。 这是必需状态。 此状态必须定义以下五个用户操作：

      * 将文档状态更改为 *在Adobe Sign Authoring中* 状态。 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 将文档状态更改为 *处于Adobe签名状态*&#x200B;的 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 将文档状态更改为 *Adobe Sign Cancelled* 状态。 对于任何生命周期的所有文档类型，此用户操作的名称必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 调用Web操作“Adobe Sign”的操作。
      * 调用Web操作“取消Adobe Sign”的操作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑字段、编辑关系、下载源、管理可查看的呈现形式以及更改状态。

      ![生命周期状态2的图像](images/lifecycle-state2.png)

   * **在Adobe Sign Authoring中**:这是指示文档已上载到Adobe Sign及其协议处于AUTHORING或DOCUMENTS_NOT_YET_PROCESSED状态的状态的状态的占位符名称。 这是必需状态。 此状态必须定义了以下四个用户操作：

      * 将文档状态更改为“Adobe Sign已取消”状态的操作。 无论生命周期如何，此用户操作的名称对于所有文档类型都必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 将文档状态更改为“进行Adobe签名”状态的操作。 无论生命周期如何，此用户操作的名称对于所有文档类型都必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 调用Web操作“Adobe Sign”的操作
      * 调用Web操作“取消Adobe Sign”的操作。 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑字段、编辑关系、下载源、管理可查看的呈现形式以及更改状态。

      ![生命周期状态3的图像](images/lifecycle-state3.png)

   * **Adobe签名**:这是指示文档已上载到Adobe Sign且其协议已发送给参与者的状态的占位符名称（OUT_FOR_SIGNATURE或OUT_FOR_APPROVAL状态）。 这是必需状态。 此状态必须定义了以下五个用户操作：

      * 将文档状态更改为“Adobe Sign已取消”状态的操作。 此操作的目标状态可以是任何客户要求，也可以是不同类型的不同状态。 无论生命周期如何，此用户操作的名称对于所有文档类型都必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 将文档状态更改为“Adobe Sign已拒绝”状态的操作。 此操作的目标状态可以是任何客户要求，也可以是不同类型的不同状态。 无论生命周期如何，此用户操作的名称对于所有文档类型都必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 将文档状态更改为“Adobe签名”状态的操作。 此操作的目标状态可以是任何客户要求，也可以是不同类型的不同状态。 但是，无论生命周期如何，此用户操作的名称对于所有文档类型都必须相同。 如有必要，可将此操作的条件设置为“允许Adobe Sign用户操作等于是”。
      * 调用Web操作的操作 *Adobe Sign*&#x200B;的
      * 调用Web操作的操作 *取消Adobe Sign*&#x200B;的 此状态必须具有允许Adobe Sign管理员角色执行以下操作的安全性：查看文档、查看内容、编辑字段、编辑关系、下载源、管理可查看的呈现形式以及更改状态。

      ![生命周期状态4的图像](images/lifecycle-state4.png)

      * **Adobe已签名（已批准）**:这是一个占位符名称，表示已将文档上传到Adobe Sign并且其协议已完成（处于已签名或批准状态）的状态的文档。 它是必需状态，并且可以是现有的生命周期状态，例如“已批准”。
此状态不需要用户操作。 其安全性必须允许Adobe Sign管理员角色：查看文档、查看内容和编辑字段。

   下图说明了Adobe Sign协议与Vault文档状态之间的映射，其中“Adobe签名前”状态为“草稿”。

   ![图像](images/sign-vault-mappings.png)

### 步骤 11. 将Adobe Sign阶段添加到生命周期阶段组中的常规生命周期

![图像](images/add-adobe-sign-stage.png)

### 步骤 12. 设置用户角色在生命周期状态下的权限

您必须在“生命周期状态”为每个用户角色设置相应的权限，如下图所示。

![图像](images/set-user-role-permissions.png)

### 步骤 13. 根据文档状态和用户角色设置原子安全

![图像](images/set-atomic-security.png)

### 步骤 14. 创建文档消息以取消Adobe Sign

![图像](images/create-cancel-message.png)

## Connect [!DNL Veeva Vault] 到Adobe Sign的中间件 {#connect-middleware}

完成设置后 [!DNL Veeva Vault] 对于Adobe Sign管理员帐户，管理员必须使用中间件在两个帐户之间建立连接。 在 [!DNL Veeva Vault] 和Adobe Sign帐户连接由Adobe Sign Identity启动，然后用于存储[!DNL Veeva Vault]身份。
为了系统安全和稳定，管理员必须使用专用的 [!DNL Veeva Vault] 系统/服务/实用程序帐户，例如 `adobe.for.veeva@xyz.com`而不是个人用户帐户，例如 `bob.smith@xyz.com`的

Adobe Sign帐户管理员必须按照以下步骤进行连接 [!DNL Veeva Vault] 到Adobe Sign使用中间件：

1. 转到 [适用于 [!DNL Veeva Vault] 主页](https://static.adobesigncdn.com/veevavaultintsvc/index.html)的
1. 选择 **[!UICONTROL 登录]** （位于右上角）。

   ![中间件登录图像](images/middleware_login.png)

1. 在打开的Adobe Sign登录页面中，提供帐户管理员电子邮件地址和密码，然后选择 **[!UICONTROL 登录]**&#x200B;的

   ![图像](images/middleware-signin.png)

   成功登录后，页面会显示关联的电子邮件ID和设置选项卡，如下所示。

   ![图像](images/middleware_settings.png)

1. 选择 **[!UICONTROL 设置]** 选项卡。

   “设置”页面显示可用的连接，并显示 *无可用连接* 如果是首次连接设置，如下所示。

   ![图像](images/middleware_newconnection.png)

1. 选择 **[!UICONTROL 添加连接]** 以添加新连接。

1. 在打开的“添加连接”对话框中，提供所需的详细信息，包括 [!DNL Veeva Vault] 凭据。

   Adobe Sign凭据从最初的Adobe Sign登录中自动填充。

   ![图像](images/middleware_addconnection.png)

1. 选择 **[!UICONTROL 验证]** 以验证帐户详细信息。

   成功验证后，您会看到“用户验证成功”通知，如下所示。

   ![图像](images/middleware_validated.png)

1. 要限制特定Adobe Sign组的使用，请展开 **[!UICONTROL 编组]** 下拉列表，然后选择其中一个可用组。

   ![图像](images/middleware_group.png)

1. 要将审计报告附加到已签名格式副本，请选中复选框 **[!UICONTROL 将审核报告附加到已签名的呈现形式]**&#x200B;的

   ![图像](images/add-audit-report.png)

1. 要允许在Adobe Sign中自动设置用户，请选中复选框 **[!UICONTROL 自动设置Sign用户]**&#x200B;的

   **注意：** 只有在启用新Adobe Sign用户之外，还在Adobe Sign的Adobe Sign帐户级别中启用了该新用户后，该新用户才会自动设置 **[!UICONTROL 自动设置Sign用户]** 对于[!DNL Veeva Vault]Adobe Sign集成，由Adobe Sign帐户管理员如下所示。

   ![图像](images/allow-auto-provisioning.png)

1. 选择 **[!UICONTROL 保存]** 以保存新连接。

   新连接将显示在“设置”选项卡下，其中显示了 [!DNL Veeva Vault] 和Adobe Sign。

   ![图像](images/middleware_setup.png)

