---
title: 创建 DNS 区域
description: 本主题是 Windows Server 2016 中的 IP 地址管理（IPAM）管理指南的一部分。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0ae9869b95cfa1da04e0103b5a824ff1fc21568f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814750"
---
# <a name="create-a-dns-zone"></a>创建 DNS 区域

>适用于：Windows Server（半年频道）、Windows Server 2016

你可以使用本主题通过使用 IPAM 客户端控制台来创建 DNS 区域。  
  
Administrators组成员或同等身份是执行此过程的最低要求。  
  
### <a name="to-create-a-dns-zone"></a>创建 DNS 区域  
  
1.  在服务器管理器中，单击 " **IPAM**"。 IPAM 客户端控制台随即出现。  
  
2.  在导航窗格的 "**监视和管理**" 中，单击 " **DNS 和 DHCP 服务器**"。 在 "显示" 窗格中，单击 "**服务器类型**"，然后单击 " **DNS**"。 由 IPAM 管理的所有 DNS 服务器都列在搜索结果中。  
  
3.  找到要在其中添加区域的服务器，然后右键单击该服务器。  单击 "**创建 DNS 区域**"。  
  
    ![创建 DNS 区域](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)  
  
4.  "**创建 DNS 区域**" 对话框将打开。 在 "**常规属性**" 中，选择一个区域类别和一个区域类型，然后在 "**区域名称**" 中输入一个名称。 同时，在 "**高级属性**" 中选择适用于你的部署的值，然后单击 **"确定"** 。  
  
    ![高级属性](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)  
  
## <a name="see-also"></a>另请参阅  
[DNS 区域管理](DNS-Zone-Management.md)  
[管理 IPAM](Manage-IPAM.md)  
  


