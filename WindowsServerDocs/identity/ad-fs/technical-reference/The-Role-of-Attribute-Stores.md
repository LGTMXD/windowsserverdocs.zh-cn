---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: 属性存储的角色
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 595f0b3b11172df9bf95d3bb8aab90368bb0e77f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860190"
---
# <a name="the-role-of-attribute-stores"></a>属性存储的角色
Active Directory 联合身份验证服务使用术语 "特性存储" 来指代组织用于存储其用户帐户及其相关属性值的目录或数据库。 在标识提供者组织中进行配置后，AD FS 从存储中检索这些属性值并基于该信息创建声明，以便当联合用户 \(用户（其帐户存储在标识提供者组织中\) 尝试访问应用程序或服务）时，托管在信赖方组织中的 Web 应用程序或服务可以进行适当的授权决策。  
  
有关如何生成声明的详细信息，请参阅 [The Role of Claims](The-Role-of-Claims.md)。  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>属性存储如何符合 AD FS 部署目标  
用户属性存储的位置以及用户从中进行身份验证的位置确定如何设计 AD FS 来支持用户标识。 根据属性存储所在的位置以及用户将访问 intranet 或 Internet 上的应用程序 \(\)，可以使用以下部署目标之一：  
  
-   向[你的 Active Directory 用户提供对声明感知应用程序和服务的访问权限](https://technet.microsoft.com/library/dd807071.aspx)—在此目标中，你的组织中的用户可以访问 AD FS 保护的应用程序或服务，\(你自己的应用程序或服务或合作伙伴的应用程序或服务在用户登录到公司 intranet 中的 Active Directory 时\)。  
  
-   向[你的 Active Directory 用户提供对其他组织的应用程序和服务的访问权限](https://technet.microsoft.com/library/dd807123.aspx)—在此目标中，你的组织中的用户可以访问 AD FS 保护的应用程序或服务，\(你自己的应用程序或服务或合作伙伴的应用程序或服务，\) 当用户登录到公司 intranet 中的属性存储时，以及他们从 Internet 远程登录时。  
  
-   [向另一组织中的用户提供对声明感知应用程序和服务的访问权限](https://technet.microsoft.com/library/dd807099.aspx)-在此目标中，另一个组织中位于该组织企业 intranet 上属性存储中的用户帐户必须访问你组织中受 AD FS 保护的应用程序。 如果在组织的外围网络中的属性存储中的基于使用者\-的用户帐户必须能够访问组织中受 AD FS 保护的应用程序，则此目标也适用。  
  
根据属性存储放置和组织的其他要求，你可以将这些部署目标中的若干个目标组合在一起，以完成你的 AD FS 部署的设计。  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS 支持的属性存储  
AD FS 支持范围广泛的目录和数据库存储，可以使用它们来提取管理员\-定义的属性值并使用这些值填充声明。 AD FS 支持任何以下目录或数据库作为属性存储：  
  
-   Windows server 2003 中的 Active Directory，Active Directory 域服务 windows server 2008 中 \(AD DS\)，Windows Server 2012 和 2012 R2，以及 Windows Server 2016。 
  
-   所有版本的 Microsoft SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014 和 SQL Server 2016  
  
-   自定义属性存储  
  

