---
title: Adobe Sign for NetSuite 发行说明
description: '了解当前版本的NetSuiteAdobe Sign集成中包含的新功能和更改。  '
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
source-git-commit: 924813403d8e13f816347dd548a68a16d78d866e
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 70%

---


# Adobe Sign for NetSuite 发行说明

## 更新到包v4.0.4

4.0.4 版已完全适应对所有新生成的流量使用特定于帐户的域。

Adobe Sign 图标已更新为新图形。

## 先前版本

### Adobe Sign for NetSuite 4.0.4

4.0.4 版已完全适应对所有新生成的流量使用特定于帐户的域。

Adobe Sign 图标已更新为新图形。

### Adobe Sign for NetSuite 4.0.2

重新标记为&#x200B;**Adobe Sign**(从&#x200B;*Adobe Document Cloud eSign服务*)\
您将看到&#x200B;*Adobe Sign*，您之前在其中看到&#x200B;*AdobeeSign服务*&#x200B;作为品牌重塑的证据。

### Adobe Sign for NetSuite 4.0.1

由于 NetSuite 在更新平台时引入了 API 回归错误，因此发布了这个新程序包 (v4.0.1)。

我们鼓励客户更新到最新的程序包。

### Adobe Sign for NetSuite 4.0

**增加了通过 NetSuite 自动配置用户的功能**

版本 4.0 增加了一个新的自定义首选项。如果启用这个首选项，则会为那些在 NetSuite 中发送协议的用户自动配置 Adobe Document Cloud eSign 服务用户帐户。

**已通过“为NetSuite构建”认证**

这个版本已获得“专为 Netsuite 构建”认证，并且符合所有最新的 NetSuite 设计最佳实践。

**重新命名为Adobe Document Cloud eSign服务（从EchoSign）**

您将在之前显示 Adobe EchoSign 的位置看到 Adobe Document Cloud eSign 服务（简称 Adobe eSign 服务），这表明产品已重新命名。

**使用 OAuth 实现了增强的安全性**

现在，为了提高数据安全性，eSign 服务在 NetSuite 中利用 OAuth 2.0，对 Adobe Document Cloud eSign 服务帐户进行身份验证。通过这项新协议，NetSuite 在与 eSign 服务通信时，无需请求您提供 eSign 服务密码。由于应用程序之间不能直接共享敏感信息，因此您的帐户不太可能会受到威胁。这项改进功能不会影响您的实施，但是您需要完成一次性设置来授权 NetSuite 程序包与 Adobe Document Cloud 通信。相关设置应在安装过程中完成。对于从先前版本的程序包（v3.5.9 及更低版本）升级的客户，授权过程中生成的 OAuth 令牌将替代以前使用的 API 密钥。

**将 eSign 服务从 SOAP API 迁移到 REST API**

为了提高效率、灵活性和处理速度，Adobe Document Cloud eSign服务以及NetSuite的v4.0集成已从基于SOAP的API迁移到基于REST的API。

### Adobe Sign for NetSuite 3.0

**高级参与者角色 - 审批人**

* 可将一个或多个接收者标记为协议审批人
* 审批人需要审阅和批准文档
* 批准前，审批人还需要将数据填充到协议中

**发送前预览文档或拖放表单字段**

在发送以供签名之前预览协议或拖放表单域

**向当前签名者发送提醒**

立即向当前签名者发送提醒

**高级签名者身份验证策略**

* **基于知识的身份验证：** 回答验证签名者身份的问题
   * 要求签名者通过回答从数百个公共和商业数据库提取的问题来证明自己的身份
   * 签名使用的姓名取自用户已完成身份验证的姓名，且在签名时无法更改
   * 由 RSA 提供支持
   * 每个帐户每月使用 KBA 的次数是有限的。有关更多信息，请联系销售人员。

* **Web标识：** 在签名之前，使用Facebook、LinkedIn、Google或其他第三方Web服务登录。

   * 签名者只有在使用以下第三方 Web 服务验证其身份后才能签名.
   * 签名使用的姓名取自用户的 Web 服务个人资料，且在签名时无法更改
   * 审核记录可捕获身份验证详细信息

* **一次性密码**
   * 对内部/外部签名者或所有签名者应用身份验证方法。外部签名者需要使用密码或使用基于知识的身份验证，而内部签名者则不需要

**其他自定义首选项**

* 将签名的PDF添加为指向！le URL的链接或作为NetSuite中托管的附件
* 协议签署后将审核记录添加到已签名的协议记录
* 默认情况下，将事务联系人（而不是客户电子邮件）用作第一位签名者
* 授予发件人一个选项：将接收者标记为审批人

**事务文件**

您可以使用新的“事务文件”下拉列表从当前事务中选择要附加的文件。

**所有 EchoSign 文档的 Adobe PDF 证书**

* 从EchoSign发送或下载的所有PDF文件都将通过Adobe EchoSign数字证书进行认证
* Acrobat或Reader将显示证明，以确保文档未被篡改，以增加信任和高枕无忧

**收集支持文档**

* 发件人可以在签名过程中从签名者那里收集其他支持文档（例如，驾照、经营许可证）
* 收集的文档将成为已签署协议的正式记录的组成部分

**条件数据字段**

* 定义协议字段的条件逻辑
* 条件可以基于协议中一个或多个字段的值
* 可以通过拖放表单创作 UI 或通过文本标记来定义条件
* 在根据设计的条件对文档进行签名时，签名者会收到相应的字段

**其他 EchoSign 表单字段增强**

* 下拉菜单
* 字段掩码
* 单选按钮
* 创建更短的文本标记来维护文档结构
