---
title: Adobe Sign for NetSuite发行说明
description: 了解当前版本的Adobe Sign for NetSuite集成中包括的新功能和更改。
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 6317723e-447a-4506-a621-4d967bdd6561
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Adobe Sign for NetSuite发行说明

## 更新至程序包v4.0.4

4.0.4已完全适应为所有新生成的流量使用特定于帐户的域。

Adobe Sign图标已更新为新图形。

## 早期版本

### 适用于NetSuite 4.0.4的Adobe Sign

4.0.4已完全适应为所有新生成的流量使用特定于帐户的域。

Adobe Sign图标已更新为新图形。

### 适用于NetSuite 4.0.2的Adobe Sign

重新命名为 **Adobe Sign** (来自 *Adobe Document Cloud eSign服务*)时，\
您现在看到 *Adobe Sign* 您之前所看到的 *AdobeeSign服务* 作为品牌重塑的证据。

### 适用于NetSuite 4.0.1的Adobe Sign

由于NetSuite在执行平台更新时引入了API回归错误，因此发布了一个新包(v4.0.1)。

建议客户更新到最新的程序包。

### 适用于NetSuite 4.0的Adobe Sign

**添加了通过NetSuite自动配置用户的功能**

版本4.0中添加了新的自定义首选项。启用后，在NetSuite中发送协议的用户将自动使用Adobe Document Cloud eSign服务用户帐户进行自动配置。

**通过“专为NetSuite构建”认证**

此版本获得了“专为NetSuite构建”认证，并且符合所有最新的NetSuite设计最佳实践。

**重新命名为Adobe Document Cloud eSign服务（从EchoSign）**

现在，您将在之前显示Adobe Document Cloud的位置看到Adobe EchoSign eSign服务(或简称为AdobeeSign服务)，这表明产品已重新命名。

**使用OAuth实现了增强的安全性**

为了提高数据安全性，eSign服务现在使用OAuth 2.0验证NetSuite中的Adobe Document Cloud eSign服务帐户。 通过此新协议，NetSuite可以在不请求eSign服务密码的情况下与eSign服务通信。 由于应用程序之间不会直接共享敏感信息，因此您的帐户不太可能会受到威胁。 这项改进不会影响您的实施，但是您必须执行一次性设置来授权NetSuite程序包与Adobe Document Cloud通信。 此操作将在安装过程中完成。 对于从以前版本的程序包（v3.5.9及更低版本）升级的客户，授权过程中生成的OAuth令牌将替换以前使用的API密钥。

**将eSign服务从SOAP API迁移到REST API**

为了提高效率、灵活性和处理速度，Adobe Document Cloud eSign服务（以及与NetSuite集成的版本4.0）已从SOAP的API迁移到基于REST的API。

### 适用于NetSuite 3.0的Adobe Sign

**高级参与者角色 — 审批人**

* 可将一个或多个收件人标记为协议审批人
* 审批人需要审阅并批准文档
* 审批人还需要在审批之前将数据填充到协议中

**发送前预览文档或拖放表单字段**

在发送以请求签名之前，预览协议或拖放表单字段

**向当前签名者发送提醒**

立即向当前签名者发送提醒

**高级签名者身份验证策略**

* **基于知识的身份验证：** 通过回答问题来验证签名者身份
   * 要求签名者通过回答从数百个公共和商业数据库提取的问题来证明其身份
   * 签名中的姓名取自用户已完成身份验证的姓名，且在签名时无法更改
   * 由RSA提供支持
   * 每个帐户每月使用KBA的次数是有限的。 有关更多信息，请联系销售人员。

* **Web标识：** 在签名之前，使用Facebook、LinkedIn、Google或其他第三方Web服务登录。

   * 签名者只有在使用第三方Web服务验证其身份之后才能签名。
   * 签名时姓名取自用户的Web服务个人资料，且在签名时无法更改
   * 审核记录可捕获身份验证详细信息

* **一次性密码**
   * 对内部或外部签名者或所有签名者应用身份验证方法。 外部签名者必须使用密码或使用基于知识的身份验证，而内部签名者则不需要

**其他自定义首选项**

* 将签名PDF添加为URL链接或NetSuite中托管的附件
* 协议签署后将审核记录添加到协议记录
* 默认情况下，将事务联系人用作签名者，而不是使用客户电子邮件
* 授予发件人将收件人标记为审批人的选项

**事务文件**

您可以使用新的“事务文件”下拉列表，从当前事务中选择要附加的文件。

**所有EchoSign文档的Adobe PDF认证**

* 从EchoSign发送或下载的所有PDF文件均通过Adobe EchoSign数字证书进行认证
* Acrobat或Reader会显示相关认证，保证文档未经篡改，以此来增加用户的信任并让客户放心

**收集支持文档**

* 发件人可以在签名过程中从签名者那里收集其他支持文档，如驾照、商业证书等。
* 收集的文档将成为已签署协议的正式记录的一部分

**条件数据字段**

* 定义协议字段的条件逻辑
* 条件可以基于协议中一个或多个字段的值
* 可以通过拖放表单创作UI或通过文本标记来定义条件
* 根据定义的条件对文档进行签名时，签名者会看到相应的字段

**其他EchoSign表单字段增强**

* 下拉菜单
* 字段掩码
* 单选按钮
* 创建更短的文本标记以保持文档结构
