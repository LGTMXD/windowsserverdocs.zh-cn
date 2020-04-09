---
ms.assetid: 7f285c9f-c3e8-4aae-9ff4-a9123815114e
title: 方案中心访问策略
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a22592e5c8af9fa23725de90a14a9a8a46c286d7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861150"
---
# <a name="scenario-central-access-policy"></a>方案：中央访问策略

>适用于：Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

文件的中心访问策略允许组织集中部署和管理授权策略，包括使用用户组、用户声明、设备声明和资源属性的条件表达式。 （声明是对与其关联的对象属性的断言）。 例如，若要访问严重业务影响 (HBI) 数据，用户必须是从托管设备获取访问权限并使用智能卡登录的全职员工。 这些策略在 Active Directory 域服务 (AD DS) 中定义并托管。  
  
组织访问策略由合规性和业务法规要求驱动。 例如，组织的业务要求限制对文件中个人的可识别信息 (PII) 的访问，仅文件所有者和人力资源 (HR) 部门中允许查看 PII 信息的成员可以访问，此策略适用于位于组织内文件服务器上的任意位置的 PII 文件。 在本例中，你必须能够：  
  
-   确定并标记包含 PII 的文件。  
  
-   确定允许查看 PII 信息的人力资源组成员。  
  
-   创建一个中心访问策略，适用于位于组织内文件服务器上的任意位置并且包含 PII 的所有文件。  
  
可能出于多种原因计划部署并强制执行某项授权策略，并且该策略适用于组织的多个级别。 以下是一些策略类型示例：  
  
-   **组织范围的授权策略。** 此授权策略最常由信息安全办公室发起，它由合规性或高级别的组织要求驱动并且与整个组织有关。 例如，只有全职员工才可以访问 HBI 文件。  
  
-   **部门授权策略。** 组织内的每个部门都有一些需要强制执行的特殊数据处理要求。 例如，财务部门可能希望只有财务人员才有权访问财务服务器。  
  
-   **特定的数据管理策略。** 这一策略通常与合规性和业务要求相关，其目的是保护对当前管理的信息的正确访问。 例如，金融机构可能会实施信息防护，使分析师无法访问经纪信息，而经纪人也无法访问分析信息。  
  
-   **需要知道的策略。** 此授权策略类型通常与上述策略类型一起使用。 例如，供应商应该只能访问和编辑属于他们正在处理的项目的文件。  
  
现实环境还教会我们，每个授权策略都需要有一些例外，这样，当出现重要业务需求时，组织就能快速做出反应。 例如，找不着智能卡但需要快速访问 HBI 信息的行政人员可以致电支持人员，以获取访问该信息的临时例外。  
  
中央访问策略可用作组织应用于其内部所有服务器的安全保护伞。 这些策略是对应用于文件和文件夹的本地访问策略或自定义访问控制列表 (DACL) 的补充（而非替代）。 例如，如果文件上的 DACL 允许特定用户访问，但应用于文件的中心策略禁止该用户访问，那么，该用户将无法获取对文件的访问权限。 如果中心访问策略允许访问，但 DACL 不允许访问，那么，用户同样无法获取对文件的访问权限。  
  
中心访问策略规则具有以下逻辑部分：  
  
-   **适用性。** 用于定义策略应用于哪些数据的条件，比如 Resource.BusinessImpact=High。  
  
-   **访问条件。** 包含一个或多个访问控制项 (ACE) 的列表，用于定义可访问数据的用户，比如 Allow | Full Control | User.EmployeeType=FTE。  
  
-   **例外。** 为策略定义例外的一个或多个 ACE 的附加列表，比如 MemberOf(HBIExceptionGroup)。  
  
下面两张图显示了中心访问策略和审核策略中的工作流。  
  
![解决方案指南](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide.JPG)  
  
**图 1** 中心访问策略和审核策略的概念  
  
![解决方案指南](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide_2.JPG)  
  
**图 2** 中心访问策略工作流  
  
中心授权策略由以下部分组成：  
  
-   针对特定类型的信息（如 HBI 或 PII）的一系列集中定义的访问规则。  
  
-   一个包含规则列表的集中定义的策略。  
  
-   一个分配给文件服务器上的每个文件的策略标识符，指向在访问授权过程中应该应用的特定中心访问策略。  
  
下图演示了如何将策略合并到策略列表中，以便集中控制对文件的访问。  
  
![解决方案指南](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide3.JPG)  
  
**图 3** 合并策略  
  
## <a name="in-this-scenario"></a>本方案内容  
以下中心访问策略指南可供使用：  
  
-   [规划中心访问策略部署](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)  
  
-   [部署中心访问策略&#40;演示步骤&#41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)  
  
-   [动态访问控制：方案概述](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>此方案中包含的角色和功能  
下表列出了作为本方案组成部分的角色和功能，并描述了它们如何为本方案提供支持。  
  
|角色/功能|如何支持本方案|  
|-----------------|---------------------------------|  
|Active Directory 域服务角色|Windows Server 2012 中的 AD DS 引入了基于声明的授权平台，该平台允许创建用户声明和设备声明、复合标识、（用户加设备的声明）、新的中心访问策略（CAP）模型，以及在授权决策中使用文件分类信息。|  
|文件和存储服务服务器角色|文件和存储服务提供了可帮助设置和管理一台或多台文件服务器的技术，这些服务器提供了你可在网络上集中存储文件并与用户一起共享的位置。 如果你的网络用户需要访问相同的文件和应用程序，或如果集中备份和文件管理对于你的组织非常重要，则应该通过向计算机添加文件和存储服务角色和相应的角色服务的方式，将一个或多个计算机设置为文件服务器。|  
|Windows 客户端计算机|用户可以通过客户端计算机访问网络上的文件和文件夹。|  
  


