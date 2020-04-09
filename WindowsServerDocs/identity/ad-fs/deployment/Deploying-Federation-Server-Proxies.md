---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: 部署联合服务器代理
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f348b7dbc9b786cfe401eb72b82592a51e1e6343
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855550"
---
# <a name="deploying-federation-server-proxies"></a>部署联合服务器代理

若要在 Active Directory 联合身份验证服务 \(AD FS\)中部署联合服务器代理，请完成清单中的每个任务[：设置联合服务器代理](Checklist--Setting-Up-a-Federation-Server-Proxy.md)。  
  
> [!NOTE]  
> 使用此清单时，建议您先阅读[Windows server 2012 的 "AD FS 设计指南](https://technet.microsoft.com/library/dd807036.aspx)" 中的联合服务器代理规划指南的参考，然后再开始配置服务器的步骤。 按照清单，可以更好地了解联合服务器代理的设计和部署过程。  
  
## <a name="about-federation-server-proxies"></a>关于联合服务器代理  
联合服务器代理是运行 Windows Server&reg; 2012 和已手动配置为在代理角色中操作 AD FS 软件的计算机。 你可以在组织中使用联合服务器来提供企业网络上防火墙后的 Internet 客户端和联合服务器之间的中介服务。  
  
> [!NOTE]  
> 尽管不能在同一台计算机上安装联合服务器和联合服务器代理角色，但联合服务器可以执行联合服务器代理功能。 有关详细信息，请参阅 [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx)。  
  
在 Windows Server&reg; 2012 计算机上安装 AD FS 软件并将其配置为在代理角色中服务的操作使该计算机成为联合服务器代理。  
  

