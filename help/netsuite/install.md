---
title: Adobe Sign [!DNL NetSuite]  — 安装和配置指南(v4.0.4)
description: Adobe Sign [!DNL NetSuite]  — 安装和自定义指南
product: Adobe Sign
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 378cac01-87c9-4288-8839-482121d49402
source-git-commit: 7ded835b48519cba656f160e691c697c91e2c8d0
workflow-type: tm+mt
source-wordcount: '4870'
ht-degree: 0%

---

# [!DNL NetSuite] 安装和自定义指南(v4.0.4) {#install-customize-NetSuite}

## 概览 {#overview}

Adobe Sign [!DNL NetSuite] 提供与 [!DNL NetSuite]. 您可以将Adobe Sign用于 [!DNL NetSuite] 集成将合同、报价和其他需要电子签名的文档等协议直接从收件人 [!DNL NetSuite]. 您可以创建和发送来自客户、潜在客户、报价和其他客户的Adobe Sign协议 [!DNL NetSuite] 记录。 Adobe Sign更新 [!DNL NetSuite] 并存储与 [!DNL NetSuite] 记录在完全执行后。 您可以查看从以下位置发送的所有协议的历史记录 [!DNL NetSuite] 从产品中。

请参阅 [Adobe Sign [!DNL NetSuite] 发行说明](https://experienceleague.adobe.com/docs/sign-integrations/using/netsuite/release-notes.html?lang=en) 的双曲余切值。

## 安装捆绑并配置OAuth {#install}

仅a [!DNL NetSuite] 管理员可以安装或更新捆绑。 要配置OAuth， [!DNL NetSuite] 管理员必须具有对Adobe Sign的管理员访问权限。 在您的生产帐户中安装捆绑包之前，您应先在 [!DNL NetSuite] 沙箱帐户。

请参阅 [创建Adobe Sign协议](#createagreement) 的子菜单。

>[!CAUTION]
>
>升级到v4.0.4的客户不应删除其现有API密钥。
>
>请参阅 [设置自定首选项](#configure) 有关如何使用API密钥的详细信息。

### 首次安装捆绑包

1. 导航到 [!UICONTROL **自定义> SuiteBundler >搜索和安装包**].

1. 在 *搜索和安装包* 页面，输入 **Adobe Sign** 作为关键字，选择 **[!UICONTROL 搜索]**.

1. 选择 **Adobe Sign** 包名称。

   ![搜索捆绑](images/search-for-the-bundle.png)

1. 在 *[!UICONTROL 捆绑详细信息]* 页面，选择 **[!UICONTROL 安装]**.
1. 在 *[!UICONTROL 预览捆绑安装]* 页面，选择 **[!UICONTROL 安装包]**.

   （不必更改页面上的任何默认值）

   ![安装捆绑](images/bundle-details-install.png)

1. 在出现的“安装”对话框中，选择 **[!UICONTROL 确定]** 以继续。

   在安装过程中，捆绑的状态显示为 *[!UICONTROL 待定]*.

   ![安装捆绑](images/installing-bundles.png)

1. 要显示更新状态，请选择 **[!UICONTROL 刷新]**.

   捆绑安装完成后， *Adobe Sign[!DNL NetSuite]* 在 *[!UICONTROL 已安装的包]* 的双曲余切值。

   ![已安装的包](images/installed-bundles.png)

1. 如果您已经是Adobe Sign客户帐户，请按照以下步骤执行  [安装或升级后配置OAuth](#oauth).

   如果您没有Adobe Sign帐户，则可以 [注册以获得企业试用版](https://esign.adobe.com/adobe-sign-)[!DNL NetSuite]-trial-registration.html)帐户以测试系统。 按照在线注册步骤启用Adobe Sign帐户。

## 安装或升级后配置OAuth {#oauth}

Adobe Sign使用OAuth 2.0验证您的Adobe Sign帐户 [!DNL NetSuite].

此协议授权您安装的 [!DNL NetSuite] 捆绑以与Adobe Sign通信，而无需请求密码。 由于应用程序之间不能直接共享敏感信息，因此您的帐户不太可能会受到威胁。

此身份验证不会影响您的实施，但在生产或沙箱帐户中安装或升级捆绑后，必须执行一次性配置。

在 [!DNL NetSuite] 配置OAuth的管理员还必须具有对Adobe Sign的帐户级别管理员访问权限。

1. 入 [!DNL NetSuite]，导航到 *Adobe Sign配置* 的双曲余切值。

1. 搜索 **[!UICONTROL Adobe Sign配置]** （自定义记录类型）。

1. 在“搜索结果”页中，选择 **视图** 的 *Adobe Sign配置* 记录。

   ![搜索 Adobe Sign](images/search-for-adobesignconfig.png)

1. 在“Adobe Sign配置列表”页面上，选择 **[!UICONTROL 视图]** 的 *使用OAuth访问Adobe Sign API* 记录。

   ![Adobe Sign配置列表](images/adobe-sign-configlist.png)

1. 在“Adobe Sign配置”页面上，选择 **[!UICONTROL 使用Adobe Sign登录]**

   ![登录 ](images/log-in-with-adobesign.png)

1. 在显示的Adobe Sign登录页中，输入您的凭据并选择 **[!UICONTROL 登录]**.

   ![Adobe Sign身份验证](images/8-authenticate-toadobesign-2020.png)

1. 在显示的“确认访问”页（对于OAuth）中，选择 **[!UICONTROL 允许访问]**

   ![允许访问](images/confirm-access.png)

1. 授权完成后，您将重定向回Adobe Sign Config页 [!DNL NetSuite]，如下所示。

   ![成功的OAuth](images/successful-oauth.png)

   >[!NOTE]
   >
   >在沙箱帐户中配置OAuth时，在授权完成时可能会遇到错误“无法确定客户合成ID”。
   >
   >
   >要继续，必须更改URL（系统）的帐户域部分。[!DNL NetSuite].com)，以返回 [!DNL NetSuite] 沙箱如下所示：
   >
   >
   >更改:
   >
   >
   >系统。[!DNL NetSuite].com/app/site/hosting/scriptlet.nl?script=745&amp;deploy=1&amp;web_access_point=https://echosign.com
   >
   >
   >收件人：
   >
   >
   >系统。**沙箱。**[!DNL NetSuite].com/app/site/hosting/scriptlet.nl?script=745&amp;deploy=1&amp;web_access_point=https://echosign.com

## 更新捆绑（现有用户）

[!DNL NetSuite] 捆绑更新由Adobe定期发布。 Adobe Sign的现有用户 [!DNL NetSuite] 集成可更新到最新的捆绑包。

>[!CAUTION]
>
>升级到较新版本的客户不应删除其现有的API密钥。
>
>请参阅 [设置自定义首选参数](#configure) 有关如何使用API密钥的详细信息。

### 先决条件 {#prerequisites}

更新到v4.0.4捆绑包所需的时间取决于当前具有“发出进行签名”状态的协议数量。 通常，更新100个协议需要7到10分钟。 记下要估计更新时间的记录数。

要确定发出进行签名的协议数量，请执行以下操作：

1. 导航到 **[!UICONTROL 自定义>列表、记录和文件>记录类型]**，然后查找 *Adobe Sign协议。*

   或在搜索栏中搜索Adobe Sign协议。

1. 对于 [!UICONTROL Adobe Sign协议] 记录，选择 **[!UICONTROL 搜索]**.

   ![搜索记录类型](images/search-adobe-signagreements.png)

1. 从 **[!UICONTROL 状态]** 下拉框，选择 **[!UICONTROL 发出进行签名]** 然后选择 **[!UICONTROL 提交]**.

   ![提交以供签名](images/submit-search-foragreements.png)

   记下要估计更新时间的记录数。

   ![请注意数字](images/search-results.png)

### 更新捆绑 {#updating-the-bundle}

1. 导航到 **[!UICONTROL 自定义> SuiteBundler >搜索和安装>列表]** 并找到您当前的包，如下所示。

   >[!NOTE]
   >
   >如果包有新版本，则会在 *版本* 当前包的数量。

1. 从“动作”下拉菜单中，选择 **[!UICONTROL 更新]**.

   ![更新操作](images/update-action.png)

1. 在“预览包更新”页面上，选择 **[!UICONTROL 更新包]** 而不更改页面上显示的任何默认值。

   在安装过程中，捆绑的状态显示为 *待定*.

   ![预览捆绑更新](images/preveiw-bundles-update.png).

   >[!NOTE]
   >
   >更新捆绑时，可能会收到一条警告消息，如下所示。 如果您尚未自定义 [!DNL NetSuite] 电子签名记录，您可以继续。 如果不确定，建议在沙箱帐户上安装捆绑，以在生产帐户中更新捆绑之前先对其进行测试。

   ![错误消息](images/netsuite-error.png)

1. 要显示更新状态，请选择 **[!UICONTROL 刷新]**.

   ![安装升级](images/installing-upgrade.png)

   >[!NOTE]
   >
   >如果由于与 *发出进行签名* 状态，您可以检查 **[!UICONTROL 执行日志]** 子选项卡 *Adobe Sign捆绑安装* 脚本确定更新的进度。 请参阅 [确定更新的进度](#determineprogress) 的双曲余切值。

   捆绑更新完成后， *Adobe Sign[!DNL NetSuite]* 在 *已安装的包* 的双曲余切值。

   ![已安装的包](images/4-installed-bundles.png)

## 配置捆绑 {#configure}

### 设置自定首选项  {#set-custom-preferences}

您可以使用自定义首选项来指定如何创建和存储协议 [!DNL NetSuite]. 此外， *Adobe Sign中的自动预配用户* 首选项允许您指定 [!DNL NetSuite] 当用户从Sign服务发送协议时，他们会在服务中自动设置 [!DNL NetSuite].

1. 导航到 **[!UICONTROL 设置>公司>常规首选项]**.
1. 向下滚动页面，然后选择 **[!UICONTROL 自定义首选项]** 按钮。

   ![自定义首选项](images/custom-preferences.png)

1. 根据需要启用和配置Adobe Sign首选项：

   * **输入帐户的EchoSign API密钥**:请勿在此字段中添加或编辑任何值。
   * **使用父记录联系人作为签名者**:如果启用，则在创建协议时，父记录联系人默认为第一位签名者。 发送者可以在发送之前轻松删除或编辑默认签名者，或向协议添加其他签名者。
   * **使用Trans。 如果存在，请以签名者身份联系**:仅当 *使用父记录联系人作为签名者* 首选项。 如果启用，则在从事务记录（例如，报价）生成协议时，主事务联系人默认为第一个签名者。 请参阅 [交易记录](#transrecords) 的双曲余切值。 如果没有主要事务联系人，或者如果从 [!DNL NetSuite] 对象记录（例如，客户记录、合作伙伴记录），默认收件人是客户电子邮件的主要联系人。 发送者可以在发送之前轻松删除或编辑默认签名者，或向协议添加其他签名者。
   * **允许将收件人标记为审批人**:如果启用，发送者可以将收件人标记为审批人。 标记为审批人的收件人可以审阅和批准协议，但不需要他们签名。 审批人可能需要在审批过程中将数据输入到字段中。
   * **首选协议文件夹ID**:用于指定存储最终签名协议的文件夹。 如果未为此字段设置值，则默认情况下，最终签名协议将保存在与原始文档文件相同的文件夹中。 文件夹ID必须是数字。
   * **自动附加事务PDF**:如果启用，则当从事务记录创建新协议时，事务PDF会自动附加到协议。
   * **将签名PDF添加为（附件或链接）**:如果 *列表* 从下拉菜单中选择，则“已签名”PDF会自动添加为指向该文件的链接。 如果 *附件* 从下拉菜单中选择，则签名PDF存储在 [!DNL NetSuite] 作为协议记录的附件。
   * **包含审核记录PDF和协议**:如果启用，审核记录PDF将在协议签名后自动附加到协议记录。
   * **身份验证方法适用于**:启用任何身份验证方法都指示应用标识验证方法的对象。 选项包括 *所有签名者，仅限外部签名者*&#x200B;或 *仅限内部签名者*.

   **身份验证方法** {#identity-verification-methods}

   创建协议时，可以选择启用的身份验证方法。 如果此处启用了多个身份验证方法，则Adobe Sign协议页面会显示 **[!UICONTROL 验证签名者身份]** 选项。

   * **启用签名所需的密码**:要求签名者输入您指定的一次性密码。

   * **启用基于知识的身份验证**:要求签名者提供其姓名、地址和（可选）其SSN的最后四位数字，然后回答验证他们提供的信息的问题列表。 仅在美国提供。

   * **启用Web身份验证**:要求签名者通过登录以下站点之一来验证其身份：Facebook、Google、LinkedIn、Microsoft Live、Twitter或Yahoo!。

   * **Adobe Sign中的自动预配用户**:如果启用，则发送协议的用户 [!DNL NetSuite] 会自动设置Adobe Sign用户帐户。


1. 选择 **[!UICONTROL 保存]** 来保存您的首选项。

## 配置自动状态更新 {#asu}

Adobe Sign集成捆绑包允许您在 [!DNL NetSuite] 关于已从 [!DNL NetSuite]. 启用此功能后， [!DNL NetSuite] 始终反映协议的状态。 您可以启用自动状态更新，如下所示：

1. 导航到 **[!UICONTROL 设置>公司>启用功能].**
1. 选择 **[!UICONTROL SuiteCloud]** 按钮。
1. 启用以下选项：

   * 在SuiteBuilder部分中，启用 **[!UICONTROL 自定义记录]** 选项。

   * 在SuiteScript部分中，启用 **[!UICONTROL 客户端SuiteScript]** 和 **[!UICONTROL Server SuiteScript]** 并同意两者的服务条款。

1. 选择 **[!UICONTROL 保存]**.

   您的选项将如图所示设置。

   ![启用SuiteCloud功能](images/enable-suitecloudfeatures.png)

## 对象和记录类型 {#objects}

Adobe Sign集成包已公开具有许多标准的Adobe Sign协议对象 [!DNL NetSuite] 对象，包括：客户、估计、潜在客户、业务机会和合作伙伴记录。 您也可以将Adobe Sign捆绑与其他记录类型（包括自定义记录）一起使用。

“协议”选项卡可以显示两种类型 [!DNL NetSuite] 记录：实体和事务记录。 我们通常假定交易记录是可转换为PDF文档的记录（如报价）；而“实体”记录不能转换为PDF。

## 交易记录 {#transrecords}

如果协议是从事务记录创建的，则协议记录中的第一个文档是它所来自的记录的PDF版本，而第一个收件人是记录的电子邮件地址。 如果您不希望第一个文档是它所来自的记录的PDF版本，请转到 **[!UICONTROL “设置”>“公司”>“常规首选项”>“自定义首选项”子选项卡]** 并禁用 **[!UICONTROL 自动附加事务PDF]** 选项。 请参阅 [设置自定义首选参数](#configure) 的双曲余切值。

在“自定义首选项”下，您还可以启用 **[!UICONTROL 使用Trans。 作为第一位签名者联系]** 首选项。 当与事务记录关联时，它会显示 **[!UICONTROL 协议]** 和 **[!UICONTROL Send for Signature]** 按钮。

![报价](images/quote.png)

## 实体记录 {#entity-records}

如果协议是从实体记录创建的，则第一个收件人是记录中的电子邮件地址。 与实体记录关联时，只显示“协议”选项卡。

## 自定义捆绑 {#customize}

自定义捆绑包括：

* 为“协议”子选项卡部署脚本，为相应的记录类型部署Send for Signature按钮。
* 为Adobe Sign记录类型设置角色权限。
* 修改权限以授予对 *协议* 子选项卡和 *Send for Signature* 按钮。

![脚本](images/scripts.png)

### 为其他记录类型配置Adobe Sign协议  {#configuring-adobe-sign-agreements-for-additional-record-types}

部署 *协议* 子选项卡和 *Send for Signature* 按钮：

1. 导航到 **[!UICONTROL 自定义>脚本>脚本].**

1. 在 *脚本* 列表页，找到必须部署的脚本，然后选择 ****[!UICONTROL 视图]****.

   * 添加 *Send for Signature* 按钮，选择 **[!UICONTROL Adobe Sign估计按钮]** 脚本。

   * 添加 *协议* 选项卡，选择 **[!UICONTROL Adobe Sign协议加载器]** 脚本。

1. 在“脚本”页面上，选择 **[!UICONTROL 部署脚本]**.

   ![部署脚本](images/deploly-script.png)

1. 在“脚本部署”页上，执行以下操作：

   * 从 *应用于* 列表中，选择记录类型。
   * （可选）输入脚本部署ID。

      请参阅 *创建自定义脚本部署ID* 主题 [!DNL NetSuite] 帮助中心获取更多信息。 如果未输入ID，则会生成一个ID。

   * 检查 **[!UICONTROL 已部署]** 复选框。

   ![脚本部署](images/execute-as-admin.png)

   * 设置 *状态* 到 **[!UICONTROL 已发布]**.

      您不必指定 *事件类型* 或 *日志级别*.

   * 从 [!UICONTROL *执行为角色]*下拉列表，选择 **[!UICONTROL 以管理员身份执行]**.

   * 使用 **[!UICONTROL 受众]** 子选项卡处于活动状态（默认为活动状态），请选择要授予访问权限的特定角色或用户。 如果要授予所有角色和用户的访问权限，请启用相应的 **[!UICONTROL 全选]** 选项。

   * 选择 **[!UICONTROL 保存]**. 当显示更改确认时，选择 **[!UICONTROL 返回]**.


1. 选择 **[!UICONTROL 列表]** 在“脚本部署”页面顶部返回 *脚本* 的双曲余切值。
1. 对其他脚本重复上述步骤2和3。

## 设置Adobe Sign记录类型的角色权限 {#setting-role-permissions-for-adobe-sign-record-types}

最多 [!DNL NetSuite] 角色应具有使用Adobe Sign的权限，而无需进行其他自定义。 但是，您必须为已创建的任何其他自定义角色授予权限。

1. 导航到 **[!UICONTROL 自定义>列表、记录和文件>记录类型]**.

   ![SiteBuilder — 自定义记录](images/sitebuilder-customrecords.png)

   >[!NOTE]
   >
   >如果您看不到 *记录类型* 项目，导航到 **[!UICONTROL “设置”>“公司”>“启用功能”>“Suite Cloud”选项卡]** 并启用 *自定义记录* 选项。

1. 在 *记录类型* 页面，选择 **[!UICONTROL Adobe Sign协议]** 选择

   ![协议记录类型](images/search-adobe-signagreementsforedit.png)

1. 在 *自定义记录类型* 页面，选择 **[!UICONTROL 使用权限列表]** 从 *访问类型* 下拉菜单。

   ![自定义记录类型](images/custom-record-type.png)

   >[!NOTE]
   >
   >在 *Adobe Sign协议* 记录类型是唯一需要的Adobe Sign记录类型 *使用权限列表* 访问类型。
   >
   >
   >有关设置其他Adobe Sign记录类型的访问类型的说明，请参阅步骤6。

1. 选择 **[!UICONTROL 权限]** 按钮。

   将显示角色和权限列表。

   ![角色和权限](images/roles-and-permissions.png)

1. 为添加到“[!UICONTROL Adobe Sign协议]&quot;记录类型。

   >[!NOTE]
   >
   >请参阅 *[为自定义记录类型设置权限列表](https://system)。[!DNL NetSuite].com/app/help/helpcenter.nl?fid=section_N2879931.html)* 主题 [!DNL NetSuite] 帮助中心了解更多信息

   1. 从 *角色* 的双曲余切值。
   1. 设置 *级别* 到 **[!UICONTROL 完整]**.
   1. 设置 *默认表单* 到 **[!UICONTROL 自定义EchoSign协议表单]**.
   1. 选择 **[!UICONTROL 限制表单]** 的双曲余切值。
   1. 选择 **[!UICONTROL 添加]** 以保存角色行的更改。

   ![设置权限](images/set-permissions.png)

   新行显示如下：

   ![设置协议记录类型的权限](images/set-permissions-foragreementrecordtype.png)

   对所有其他自定义角色重复上述步骤a到e。

   * 选择 **[!UICONTROL 保存]** 在 *自定义记录类型* 页面。
   在 *[!UICONTROL 客户记录类型]* 重新显示页面。

1. 重复上述步骤1到3以设置 *访问类型* 所有其他Adobe Sign记录类型

   **[!UICONTROL 无需权限].** 这适用于以下记录类型：

   * Adobe Sign配置
   * Adobe Sign 文档
   * Adobe Sign事件
   * Adobe Sign语
   * Adobe Sign脚本错误
   * Adobe Sign签名协议
   * Adobe Sign签名者

### 授予对“协议”选项卡和“Send for Signature”按钮的访问权限  {#granting-access-to-the-agreement-tab-and-send-for-signature-button}

Adobe Sign集成包已公开具有许多标准的Adobe Sign协议对象 [!DNL NetSuite] 对象(客户，估计 [报价]、潜在客户等)。 在 *协议* 子选项卡会自动为以下类型的对象启用：客户、潜在客户、业务机会、合作伙伴、潜在客户、报价和供应商账单。

在 *[!UICONTROL Send for Signature]* 按钮 **o[!UICONTROL 仅用于Quote对象]**.

[!DNL NetSuite] 管理员可以通过修改权限以添加 *协议* 子标签， *Send for Signature* 按钮，或同时显示这两个对象。

#### 修改权限以授予对Send for Signature按钮的访问权限  {#modifying-permissions-to-grant-access-to-the-send-for-signature-button}

1. 导航到 **[!UICONTROL 自定义>脚本>脚本]**.

   在 *脚本* 列表页面。

   * 如有必要，请使用滤镜来查找Adobe Sign脚本

1. 在 *脚本* 页面，找到 *Adobe Sign估计按钮* 脚本(控件 *Send for Signature* 按钮)，然后选择 **视图**.

   ![查看Adobe Sign估计按钮](images/view-adobe-sign-estimatesbutton.png)

1. 在 *脚本* ，请执行以下操作：

   * 选择 **[!UICONTROL 部署]** 子标签

   * 在“*应用于*”选择要修改的实体的链接。

      * **[!UICONTROL 报价]** 本例

   ![选择“部署”子选项卡](images/click-the-deploymentssub-tab.png)

   * 选择 **[!UICONTROL 编辑]** 按钮 *脚本部署* 页面

   ![编辑脚本部署](images/edit-script-deployment.png)

   * 使用 **[!UICONTROL 受众]** 子选项卡处于活动状态，请选择要授予访问权限的特定角色或用户。

      * 如果要授予所有角色和用户的访问权限，请启用相应的 **[!UICONTROL 全选]** 选项
   * 选择 **[!UICONTROL 保存]**

   ![选择特定角色](images/save-script-deployment-quote.png)

#### 修改权限以授予对“协议”选项卡的访问权限  {#modifying-permissions-to-grant-access-to-the-agreements-tab}

1. 导航到 **[!UICONTROL 自定义>脚本>脚本]**
1. 在 [!UICONTROL 脚本] 页面，找到 *[!UICONTROL Adobe Sign协议加载器]* 脚本(控件 *协议选项卡*)，然后选择 **[!UICONTROL 视图]**.
1. 在 *脚本* ，请执行以下操作：

   1. 选择 **[!UICONTROL 部署]** 子标签
   1. 在“*[!UICONTROL 应用于]*&#x200B;选择要修改其访问权限的实体的链接
   1. 在 *[!UICONTROL 脚本部署]* ，选择 **[!UICONTROL 编辑]** 按钮
   1. 使用 **[!UICONTROL 受众]** 子选项卡处于活动状态（默认情况下处于活动状态），请选择要授予访问权限的特定角色或用户。 如果要授予所有角色和用户的访问权限，请启用相应的 **[!UICONTROL 全选]** 选项
   1. 选择 **[!UICONTROL 保存]**

## 使用Adobe Sign [!DNL NetSuite] 捆绑

为了从 [!DNL NetSuite] 并接收这些协议的更新，用户必须在 [!DNL NetSuite] 和Adobe Sign。

### 创建Adobe Sign协议

在沙箱或生产帐户中安装新捆绑后，应通过创建新协议来测试捆绑。 您可以从实体记录、事务记录或独立协议创建Adobe Sign协议。

>[!NOTE]
>
>创建协议的过程会因协议的创建方式而稍有不同。 一般过程包括为协议指定选项、添加一个或多个协议文档以及指定收件人。 以下描述的流程假定您从客户记录中创建协议。

1. 选择或创建要从中发送协议的客户记录，或者您可以选择其他 [!DNL NetSuite] 启用了“协议”选项卡的记录类型。

1. 从记录中，选择 **[!UICONTROL 协议]** 按钮。
1. 选择 **[!UICONTROL 新建协议]**.

   ![新协议](images/new-agreement.png)

1. 在 *[!UICONTROL Adobe Sign协议]* 页面，选择 **[!UICONTROL 编辑]**.

   ![编辑新协议](images/edit-new-agreement.png)

1. 按如下方式指定协议选项：

   * **协议名称**  — 输入协议的名称。
   * **消息** — 为收件人输入自定义消息。
   * **签名类型**  — 选择文档接受的签名类型。 选项包括 *电子签名* 和 *传真签名*.

   * **我还必须签署本协议**  — 启用此选项以指示发件人还需要签署协议。
   * **签名顺序** — 如果 *我还必须签署本协议* 选项，选择发件人和收件人签名的顺序。 选项包括“我签名，收件人签名”、“收件人签名，然后我签名”和“无”。

   * **预览文档或定位签名（或表单域）**  — 启用此选项后，发送者可以预览协议，并允许他们在将协议发送给收件人之前将字段（拖放签名、初始字段和其他表单字段）添加到协议中。
   * **验证签名者身份**  — 启用此选项，然后选择以下身份验证选项之一

      * 仅当在“自定义首选项”中启用了下面列出的三种签名者身份验证方法中的一种以上时，才显示此选项。 (请参阅 [设置自定义首选参数](#customize) )。 如果仅启用一个首选项，则 **[!UICONTROL 验证签名者身份]** 选项。

   **身份验证方法**

   * **签名需要密码**  — 要求签名者输入您指定的一次性密码。
   * **基于知识的身份验证**  — 要求签名者提供其姓名、地址和SSN的最后四位数字（可选），然后回答验证他们提供的信息的问题列表。 仅在美国提供。
   * **Web身份验证**  — 要求签名者通过登录以下站点之一来验证其身份：Facebook、Google、LinkedIn、Twitter、Yahoo! 或Microsoft Live。
   * **查看密码需要密码PDF**  — 启用此选项后，将要求收件人在打开协议或已签名协议的PDF之前输入密码。 发送给每个人的PDF文件都经过加密，需要密码才能打开。 不要丢失密码，因为密码无法恢复。 如果丢失密码，必须删除该事务，然后重新开始。
   * **密码/确认密码**  — 如果 *查看密码需要密码PDF* 选项，输入用于查看协议的密码。
   * **提醒收件人签名**  — 指定是否以及向收件人发送提醒的频率。 选项包括 *从不*, *每日* 或 *每周*.
   * **语言：** 指定向收件人显示签名页面和电子邮件通知的语言。
   * **为第一位签名者托管签名**  — 启用此选项后，将允许发件人为第一位签名者托管亲临签名。
   * **签名截止日期前的天数**  — 输入整数以指示协议的签名截止日期（今天的日期+天数）。
   * **父记录**  — （可选）选择父记录以将其链接到协议。

   ![配置协议](images/configure-agreement-2.png)

1. 选择 **[!UICONTROL 文档]** 按钮。

   ![“文档”选项卡](images/documents-tab.png)

1. 在 *文档* 子选项卡，使用 *Adobe Sign文档* 下拉列表，然后选择 **[!UICONTROL 附加]**.

   或者，单击 **[!UICONTROL 新建Adobe Sign文档]** 访问 *[!UICONTROL Adobe Sign文档]* 页面，然后在 [!DNL NetSuite] 文件柜中，从事务记录中选择文件（如果适用），或附加新文档。

   您可以向协议中添加多个文档。

1. 选择 **[!UICONTROL 收件人]** 选项卡，然后通过从联系人列表中选择或键入电子邮件地址来指定收件人。

   ![添加收件人](images/add-recipients.png)

   您的每个收件人都可以标记为“签名者”或“抄送”。 如果 *允许将收件人标记为审批人签名者* 启用“自定义”首选项，收件人也可以标记为“审批人”。 请参阅 [设置自定义首选参数](#customize) 的双曲余切值。

   * **签名者** 必须签署协议。
   * **审批人** 必须批准协议，但不签署协议，并且可能还必须向协议添加数据。
   * **CCd收件人** 将在协议更新和协议签署和完成时收到通知。 CC收件人不是签名或审批流程的参与方。

      如果 *使用父记录联系人作为签名者* 自定义首选项是单独启用的，还是与 *使用Trans。 以签名者身份联系* 首选项，第一个收件人是默认收件人，但可以更改。

1. 选择 **[!UICONTROL 添加]** 输入每个收件人后。

1. 选择 **[!UICONTROL 保存]** 以保存协议。

### 发送协议以供签名

当协议准备好发送时，选择 **[!UICONTROL Send for Signature]** 按钮。

* 如果 *预览文档或定位签名* 选项，单击 **[!UICONTROL Send for Signature]**. 在打开的窗口中，预览文档或将表单域拖动到文档，然后再发送文档。 选择 **[!UICONTROL 发送]** 将协议发送给收件人。

* 如果 *[!UICONTROL 为第一位签名者托管签名]* 选项，单击 **[!UICONTROL Send for Signature]**. 在打开的窗口中，允许签名者使用发件人签名文档。

   A *为当前签名者托管签名* 链接也显示在 *为第一位签名者托管签名* 字段，可在文档签名之前访问。 使用此链接可托管多个签名者的协议签名，或者在弹出窗口意外关闭时重新打开该窗口。

在发送协议后，收件人会收到一封电子邮件，通知他们等待其签名的文档。

在收件人签名文档后，发件人会通过电子邮件收到文档已签名的通知。

#### 从报价发送

Adobe Sign直接与 [!DNL NetSuite] 以便自动生成报价PDF并附加到协议记录。

查看报价时，选择 **[!UICONTROL Send for Signature]**. 它生成并显示附加到协议的报价。 您还可以添加 *Send for Signature* 按钮。 请参阅 [对象和记录类型](#objects) 的双曲余切值。

![报价 — Send for Signature](images/quote-send-forsignature.png)

### 跟踪状态和发送提醒

发送协议后：

* 文档状态更改为 *发出进行签名* 在“协议详细信息”部分
* 在 *Send for Signature* 按钮由以下三个按钮替换：

   * **更新状态**  — 如果尚未配置状态更新，请手动更新状态。 请参阅 [配置自动状态更新](#asu) 的双曲余切值。
   * **发送提醒**  — 向当前签名者发送提醒。
   * **取消协议**  — 取消协议。 如果所有收件人尚未签名，则协议在发送以请求签名后可能会被取消。

![已发出进行签名](images/out-for-signature.png)

新 *事件* 子选项卡显示在协议记录中，您可以在其中跟踪协议的状态。

您可以查看协议事件的历史记录，其中包括有关协议何时发送、查看和签名的信息。

![签名协议事件](images/agreement-events.png)

协议签署后：

* 其状态更改为 *已签名*.
* 您可以使用该链接链接返回到此协议的父记录。
* 您可以使用签名文档和审核记录下的“下载”链接访问这些文档。
* 附加 *签名文档* “子”选项卡显示以查看签名文档的缩览图。

![已签名协议](images/signed-agreement.png)

>[!NOTE]
>
>在发送协议以请求签名后，您无法编辑记录。 这是为了保留事件的记录。

## 卸载捆绑

要卸载捆绑，请按照 [!DNL NetSuite] 帮助。 请参阅 *[卸载捆绑](https://docs.oracle.com/cloud/latest/)[!DNL NetSuite]cs_gs/NSBDL/NSBDL.pdf)* 主题 [!DNL NetSuite] 帮助中心获取更多信息。

卸载捆绑包时，将删除未签名的协议。 签名的协议及其相应的审核PDF文件不受影响。

如果必须保留未签名的协议，请不要卸载捆绑包。

## 疑难解答

### 确定更新的进度

如果更新的时间似乎超过，您可以检查Adobe Sign捆绑安装脚本的“执行日志”子选项卡，以确定更新的进度，如下所示：

1. 导航到 **[!UICONTROL 自定义>脚本>脚本]**.
1. 在 [!UICONTROL 脚本] 页面，找到 *[!UICONTROL Adobe Sign捆绑安装]* 脚本，然后选择 **[!UICONTROL 编辑]**.
1. 在 [!UICONTROL 脚本] ，选择 **执行日志** 按钮。
1. 选择 **刷新**.

   执行日志将更新以反映状态。 在 *详细信息* 列显示对协议的更新进度。

   ![刷新进度](images/refresh-progress.png)

### 解决访问令牌问题

在与协议交互时，您可能会遇到“提供的访问令牌无效或已过期”消息。

这可能由于以下原因而发生：

* 在 [!DNL NetSuite]/Adobe Sign管理员（配置了OAuth）已吊销访问令牌
* 访问令牌已过期，因为尚未发送协议 [!DNL NetSuite] 过去60天里
* 在 [!DNL NetSuite]/Adobe Sign管理员未成功完成初始OAuth配置

要解决此问题，请再次执行OAuth配置进程。 请参阅 [在安装或升级后配置OAuth](#oauth) 的双曲余切值。

![令牌无效](images/invalid-token.png)

### 解决文档状态问题 {#resolvestatus}

如果 [自动状态更新](#asu) 已配置，但协议状态在发送协议后未更新，请尝试以下操作：

1. 检查部署执行日志 *Adobe Sign外部更新* 脚本，查看您是否接收来自Adobe Sign的呼叫，如下所示：

   1. 导航到 **[!UICONTROL 自定义>脚本>脚本部署]**
   1. 在 *脚本部署* 页面，找到 *Adobe Sign外部更新* 脚本，然后选择 **[!UICONTROL 编辑]**
      1. 在 *[!UICONTROL 脚本部署]* ，选择 **[!UICONTROL 执行日志]** 按钮。
      * 您应该看到 *更新的协议记录* 每个协议ID的条目


1. 检查部署执行日志 *Adobe Sign更新协议* 脚本，查看是否存在以下错误：

   1. 导航到 **[!UICONTROL 自定义>脚本>脚本部署]**.
   1. 在 [!UICONTROL 脚本部署] 页面，找到 *[!UICONTROL Adobe Sign更新协议]* 脚本[!UICONTROL 已计划]状态，然后选择 **[!UICONTROL 编辑]**.
   1. 在 [!UICONTROL 脚本部署] ，选择 **[!UICONTROL 执行日志]** 按钮。
   1. 在 [!UICONTROL 文字]，选择 **[!UICONTROL 错误]** 来筛选结果。

1. 最后，检查执行日志 *Adobe Sign Manager* 按照以上步骤2中的说明编写错误脚本。

### 解决MIME类型错误  {#resolving-mime-type-errors}

如果在发送协议时遇到MIME类型错误，可能是因为“文件名”字段中的名称与已上载文件的文件名和扩展名不匹配。 如果将“文件名”字段留空，将自动使用正确的文件名和扩展名填充。

### 查看脚本日志 {#viewing-script-logs}

您还可以查看与文档状态问题无关的脚本的部署执行日志。 请参阅 [解决文档状态问题](#resolvestatus) 的双曲余切值。

1. 导航到 **[!UICONTROL 自定义>脚本>脚本]**.

   在 *脚本* 列表页面。 如有必要，请使用滤镜来查找相应的脚本。

1. 选择 **[!UICONTROL 视图]** 对应脚本。

1. 选择 **[!UICONTROL 执行日志]** 的子选项卡。

## 支持 {#support}

转到 [Adobe Sign支持门户](https://adobe.com/go/adobesign-support-center_cn) 访问常见问题解答、文档、知识库文章或联系Adobe支持。
