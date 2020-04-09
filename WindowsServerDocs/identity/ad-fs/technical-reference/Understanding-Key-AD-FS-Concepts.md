---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: 了解关键 Active Directory 联合身份验证服务概念
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ba0ad6cd0f081797ffcb9bae2416b556de16622c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853830"
---
# <a name="understanding-key-ad-fs-concepts"></a>了解关键的 AD FS 概念
建议你了解 Active Directory 联合身份验证服务的重要概念并熟悉其功能集。  
  
> [!TIP]  
> 可以在 Microsoft TechNet Wiki 上的 [AD FS 内容导航图](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) 页面中找到更多 AD FS 资源链接。 此页面由 AD FS 社区的成员管理，并由 AD FS 产品团队定期进行监视。  
  
## <a name="ad-fs-terminology-used-in-this-guide"></a>本指南中使用的 AD FS 术语  
  
|AD FS 术语|Definition|  
|--------------|--------------|  
|帐户伙伴组织|由联合身份验证服务中的声明提供方信任表示的联合身份验证伙伴组织。 帐户伙伴组织包含将访问 Web 的用户\-基于资源伙伴中的应用程序。|  
|帐户联合身份验证服务器|帐户伙伴组织中的联合服务器。 帐户联合服务器基于用户身份验证向用户颁发安全令牌。 服务器对用户进行身份验证、从属性存储中提取相关属性和组成员身份信息、将此信息打包到声明中，并生成和签名安全令牌 \(包含要返回给用户的声明\) （要在其自己的组织中使用，或者发送到伙伴组织）。|  
|AD FS 配置数据库|一个数据库，用于存储表示单个 AD FS 实例或联合身份验证服务的所有配置数据。 此配置数据可以存储在 SQL Server 数据库中，也可以使用 Windows Server 2016、Windows Server 2012 和 2012 R2 随附的 Windows 内部数据库功能，以及 Windows Server 2008 和 2008 R2。 </br></br>您可以使用 Fsconfig.exe 命令\-行工具创建 SQL Server 的 AD FS 配置数据库，并使用 AD FS 联合服务器配置向导为 Windows 内部数据库创建此数据库。|  
|声明提供方|向其用户提供声明的组织。 请参阅帐户伙伴组织。|  
|声明提供方信任|在中的 AD FS 管理 "管理单元\-中，声明提供方信任是通常在资源伙伴组织中创建的信任对象，用于在信任关系中表示其帐户将访问资源伙伴组织中的资源的组织。 声明提供方信任对象包含各种标识符、名称和用于在本地联合身份验证服务中标识此伙伴的规则。|  
|本地声明提供程序信任|一个信任对象，表示 AD FS 场中基于 AD LDS 或第三\-方 LDAP\-目录。 本地声明提供程序信任对象包含各种标识符、名称和规则，用于标识此 LDAP\-基于的目录到本地联合身份验证服务。|  
|联合元数据|用于在声明提供方和信赖方之间通信配置信息，以便正确配置声明提供方信任和信赖方信任的数据格式。 数据格式在安全断言标记语言 \(SAML\) 2.0 中定义，并在 WS\-联合中进行扩展。|  
|联合身份验证服务器|已使用 AD FS 联合服务器配置向导进行配置以充当联合服务器角色的 Windows Server。 联合服务器颁发令牌并充当联合身份验证服务的一部分。|  
|联合身份验证服务器代理|已使用 AD FS 联合服务器代理配置向导进行配置，以充当 Internet 客户端和位于企业网络防火墙后面的联合身份验证服务之间的中间代理服务的 Windows 服务器。|  
|主联合服务器|在联合服务器角色中使用 AD FS 联合服务器配置向导配置的 Windows Server，并且具有 AD FS 配置数据库的读取\/写入副本。 </br></br> 当你使用 AD FS 联合服务器配置向导并选择创建新联合身份验证服务的选项并使该计算机成为服务器场中的第一台联合服务器时，将创建主联合服务器。 此服务器场中的所有其他联合服务器必须将主联合服务器上所做的更改复制到本地存储的 AD FS 配置数据库的读取\-副本。 当 AD FS 配置数据库存储在 SQL 数据库中时，术语 "主联合服务器" 不适用，因为所有联合服务器都可以对存储在 SQL Server 上的配置数据库进行同样的读取和写入。|  
|依赖方 (Relying party)|接收和处理声明的组织。 请参阅资源伙伴组织。|  
|依赖方信任 (Relying party trust)|在的 AD FS 管理 "管理单元\-中，信赖方信任是通常在中创建的信任对象：<p>-用于在信任关系中表示组织的帐户伙伴组织，其帐户将访问资源伙伴组织中的资源。<br />-资源伙伴组织，用于表示联合身份验证服务与单个基于 web\-的应用程序之间的信任。<p>信赖方信任对象包含各种标识符、名称和规则，用于识别本地联合身份验证服务的此伙伴或 web\-应用程序。|  
|资源联合身份验证服务器|资源伙伴组织中的联合服务器。 资源联合服务器通常基于由帐户联合服务器颁发的安全令牌向用户颁发安全令牌。 服务器接收安全令牌、验证签名、将声明规则逻辑应用到未打包的声明以产生所需的传出声明，基于传入安全令牌中的信息生成新的安全令牌 \(与传出声明\)，并签署新令牌以返回到用户并最终返回到 Web 应用程序。|  
|资源伙伴组织|由联合身份验证服务中的信赖方信任表示的联合身份验证伙伴。 资源伙伴\-基于声明的安全令牌发出声明，其中包含帐户伙伴中的用户可以访问的基于 Web\-发布的应用程序。|  
  
## <a name="overview-of-ad-fs"></a>AD FS 概述  
AD FS 是一种标识访问解决方案，该解决方案向网络\) 提供客户端计算机 \(内部或外部，\-并且即使用户帐户和应用程序位于完全不同的网络或组织中。  
  
当应用程序或服务在一个网络中，而用户帐户处于另一个网络中时，用户尝试访问应用程序或服务时通常会被提示输入辅助凭据。 这些辅助凭据表示应用程序或服务所驻留的领域中的用户身份。 托管应用程序或服务的 Web 服务器通常需要使用它们，以便该服务器可以做出最适当的授权决策。  
  
使用 AD FS，组织可以通过提供信任关系 \(联合身份验证信任，绕过辅助凭据的请求\) 这些组织可使用这些信任关系将用户的数字标识和访问权限投影到受信任的伙伴。 在此联合环境中，每个组织继续管理自己的标识，但每个组织还可以安全地投影和接受来自其他组织的标识。  
  
-   [属性存储的角色](The-Role-of-Attribute-Stores.md)  
  
-   [AD FS 配置数据库的角色](The-Role-of-the-AD-FS-Configuration-Database.md)  
  
-   [声明的角色](The-Role-of-Claims.md)  
  
-   [声明规则的角色](The-Role-of-Claim-Rules.md)  
  
-   [声明引擎的角色](The-Role-of-the-Claims-Engine.md)  
  
-   [声明管道的角色](The-Role-of-the-Claims-Pipeline.md)  
  
-   [声明规则语言的角色](The-Role-of-the-Claim-Rule-Language.md)  
  
-   [确定要使用的声明规则模板的类型](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)  
  
-   [在 AD FS 中如何使用 URI](How-URIs-Are-Used-in-AD-FS.md)  
  

