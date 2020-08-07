---
ms.assetid: 696a29b2-d627-4c9a-a384-9c8aaf50bd23
title: 确定要使用的声明规则模板的类型
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: bbc73c48fa3c1dd4bb743d5c088fdd94d722d5a1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938018"
---
# <a name="determine-the-type-of-claim-rule-template-to-use"></a>确定要使用的声明规则模板的类型


设计 Active Directory 联合身份验证服务 AD FS 基础结构的一个重要部分 \( \) 是确定一组完整的声明规则，以及你应用于创建这些规则的相应声明规则模板（适用于将参与组织的联合的每个合作伙伴）。 在 AD FS 管理 "管理单元中使用声明规则模板创建规则 \- 。

你配置的每组声明规则只能与一个联合信任相关联。 这意味着，你不能在一个信任上创建一组规则，但将其用于联合身份验证服务中的其他信任。 不过，你可以根据声明规则模板轻松地创建规则，从而有助于更快地生成一组所需的声明，并且这些声明得到每位联盟伙伴和组织的一致同意。

有关规则和规则模板的详细信息，请参阅 [The Role of Claim Rules](The-Role-of-Claim-Rules.md)。

在开始确定应使用的声明规则模板类型之前，请考虑以下问题：

-   你的可信声明提供程序将提供哪些声明？

-   你信任每个声明提供程序的哪些声明？

-   信任此联合身份验证服务的信赖方需要哪些声明？

-   你愿意向每个信赖方公开哪些声明？

-   哪些用户将有权访问每个信赖方？

回答这些问题将有助于制定一个可靠的声明规则设计。 此外，还有助于创建平稳的授权和访问控制策略，让你的部署团队在产品推出期间更高效。

在下一部分中，你可以了解要根据业务需求为环境选择的规则模板类型。

## <a name="claim-rule-template-types"></a>声明规则模板类型
下表描述了可用于使用 AD FS 管理 "管理单元创建规则的所有声明规则模板类型 \- ，以及使用一种模板类型的优势。

|规则模板类型|描述|优点|缺点|
|----------------------|---------------|--------------|-----------------|
|通过或筛选传入声明|用于创建一项规则，该规则将传递所选声明类型的所有声明值，或者根据声明值筛选声明，以便仅传递所选声明类型的某些声明值。<p>有关详细信息，请参阅 [When to Use a Pass Through or Filter Claim Rule](When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)。|-可用于选择要接受或发出不变的特定声明|-不能更改声明的类型和值|
|转换传入声明|用于创建一项规则，该规则可以选择一个传入声明并将其映射到不同的声明类型或将其声明值映射到新的声明值。<p>有关详细信息，请参阅 [When to Use a Transform Claim Rule](When-to-Use-a-Transform-Claim-Rule.md)。|-可用于规范化声明类型或值<br />-可以替换 \- 传入声明的电子邮件后缀|-更复杂的字符串替换需要自定义规则|
|以声明方式发送 LDAP 属性|用于创建一项规则，该规则将从 LDAP 属性存储中选择要以声明方式发送给信赖方的属性。<p>有关详细信息，请参阅 [When to Use a Send LDAP Attributes as Claims Rule](When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)。|-可以从任何 AD DS \/ AD LDS 属性存储的源声明<br />-可以使用单个规则发出多个声明|-性能-因帐户查找而慢<br />-不能将自定义 LDAP 筛选器用于查询|
|以声明方式发送组成员身份|用于创建一项规则，当用户是 Active Directory 安全组的成员时，该规则可以发送指定的声明类型和值。 根据所选择的组，将使用此规则仅发送一个声明。<p>有关详细信息，请参阅 [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)。|-发出组声明的快速性能-无帐户查找|-用户必须是本地 Active Directory 组的成员|
|使用自定义规则发送声明|用于创建一项自定义规则，该规则将提供比标准规则模板更高级的选项。 您可以用 AD FS 声明规则语言编写自定义规则。<p>有关详细信息，请参阅 [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md)。|-可用于从 SQL 特性存储源声明<br />-可用于指定自定义 LDAP 筛选器<br />-可用于发出 PPID<br />-可与自定义属性存储一起使用<br />-只能用于向输入声明集添加声明<br />-可用于基于多个传入声明发送声明|-若要开始了解 \- 声明规则语言，则可能需要更难配置某些加速时间|
|根据传入声明允许或拒绝用户|用于创建创建一项规则，该规则将根据传入声明的类型和值，允许或拒绝用户访问信赖方。<p>有关详细信息，请参阅 [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md)。|-简化了授权过程|-要求仅指定一个声明类型和一个声明值<br />-不支持声明值的模式匹配|
|允许所有用户|用于创建一项规则，该规则将允许所有用户访问信赖方。<p>有关详细信息，请参阅 [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md)。|-简单配置|-不如使用根据传入声明模板允许或拒绝用户的安全|


