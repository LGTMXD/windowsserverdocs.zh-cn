---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: 将部署目标映射到 AD FS 设计
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4154f46bdb1a7b3a2c81eba6882a6a095a16ee45
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853050"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>将部署目标映射到 AD FS 设计


查看完现有 Active Directory 联合身份验证服务 \(AD FS\) 部署目标并确定哪些目标与部署相关后，可以将这些目标映射到特定的 AD FS 设计。 有关 AD FS 预定义部署目标的详细信息，请参阅[确定 AD FS 部署目标](Identifying-Your-AD-FS-Deployment-Goals.md)。  
  
使用下表来确定哪个 AD FS 设计映射到组织 AD FS 部署目标的适当组合。 此表只引用了这两个主要 AD FS 设计，如本指南中所述。 不过，你可以通过使用 AD FS 部署目标的任意组合来创建混合或自定义 AD FS 设计，以满足你的组织的需求。  
  
|AD FS 部署目标|[Web SSO 设计](Web-SSO-Design.md)|[联合 Web SSO 设计](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[为声明感知应用程序和服务提供 Active Directory 用户访问权限](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|是|是，在帐户伙伴中|  
|[为其他组织的应用程序和服务提供 Active Directory 用户访问权限](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|是|是，在帐户伙伴中（可选）|  
|[为另一个组织中的用户提供对声明感知应用程序和服务的访问权限](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|是|是|  

## <a name="see-also"></a>另请参阅
[Windows Server 2012 中的 AD FS 设计指南](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

