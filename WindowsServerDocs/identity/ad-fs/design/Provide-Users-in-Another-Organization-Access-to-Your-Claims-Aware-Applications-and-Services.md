---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: 为另一个组织中的用户提供对声明感知应用程序和服务的访问权限
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 03b9e4142d522ce8a455bb9cb18dbae48a89f302
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969734"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>为另一个组织中的用户提供对声明感知应用程序和服务的访问权限


如果你是 Active Directory 联合身份验证服务 AD FS 的资源伙伴组织中的管理员 \( \) ，并且你的部署目标是为另一个组织中的用户提供对另一组织中的用户的联合访问权限。 \( \) \- \- \( \)

-   你的组织中的联合用户和已配置为组织帐户伙伴组织的联合信任的组织中的联合用户 \( \) 可以访问由你的组织托管的受 AD FS 保护的应用程序或服务。 有关详细信息，请参阅 [Federated Web SSO Design](Federated-Web-SSO-Design.md)。

    例如，Fabrikam 可能希望其企业网络员工对 Contoso 中托管的 Web 服务具有联合访问权限。

-   与受信任组织没有直接关联的联合用户（ \( 如个人客户 \) ）将登录到在外围网络中托管的属性存储，可以 \- 通过从位于 Internet 上的客户端计算机登录一次来访问多个 AD FS 受保护的应用程序，这些应用程序也托管在外围网络中。 换句话说，当你托管客户帐户以实现对外围网络中的应用程序或服务的访问时，你在属性存储中托管的客户只需登录一次，便可访问外围网络中的一个或多个应用程序或服务。 有关详细信息，请参阅 [Web SSO Design](Web-SSO-Design.md)。

    例如，Fabrikam 可能希望其客户对 \- \- \( \) 其外围网络中托管的多个应用程序或服务具有单一登录 SSO 访问权限。

此部署目标需要以下组件：

-   **Active Directory 域服务 \(AD DS \) ：** 资源伙伴联合服务器必须加入 Active Directory 域。

-   **外围 DNS：** 域名系统 \( DNS \) 应该包含一个简单的主机 \( a \) 资源记录，以便客户端计算机可以找到资源伙伴联合服务器和 Web 服务器。 DNS 服务器可以托管在外围网络中也需要的其他 DNS 记录。 有关详细信息，请参阅[联合服务器的名称解析要求](Name-Resolution-Requirements-for-Federation-Servers.md)。

-   **资源伙伴联合服务器：** 资源伙伴联合服务器验证帐户伙伴发送 AD FS 令牌。 帐户伙伴发现是通过此联合服务器执行的。 有关详细信息，请参阅 [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)。

-   **Web 服务器**：Web 服务器可以托管 Web 应用程序或 Web 服务。 Web 服务器先确认它从联合用户收到有效 AD FS 令牌，然后才允许访问受保护的 Web 应用程序或 Web 服务。

    通过使用 Windows Identity Foundation \( WIF \) ，你可以开发 Web 应用程序或服务，以便它能够接受使用任何标准登录方法（如用户名和密码）进行的联合用户登录请求。

在查看链接的主题中的信息后，可以按照清单中的步骤开始部署此目标[：实现联合 WEB Sso 设计](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)和[清单：实现 Web sso 设计](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)。

下图显示了此 AD FS 部署目标所需的每个组件。

![对声明的访问权限](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)

## <a name="see-also"></a>另请参阅
[Windows Server 2012 中的 AD FS 设计指南](AD-FS-Design-Guide-in-Windows-Server-2012.md)
