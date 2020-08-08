---
title: 为 DNS 区域设置访问范围
description: 本主题是 Windows Server 2016 中的 IP 地址管理 (IPAM) 管理指南的一部分。
manager: brianlic
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 155e21bae4045f094696a8193966469f09a8b6ea
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944659"
---
# <a name="set-access-scope-for-a-dns-zone"></a>为 DNS 区域设置访问范围

>适用于：Windows Server（半年频道）、Windows Server 2016

你可以使用本主题通过使用 IPAM 客户端控制台来设置 DNS 区域的访问作用域。

Administrators**** 组成员或同等身份是执行此过程的最低要求。

### <a name="to-set-the-access-scope-for-a-dns-zone"></a>设置 DNS 区域的访问作用域

1.  在服务器管理器中，单击 " **IPAM**"。 IPAM 客户端控制台随即出现。

2.  在导航窗格中，单击 " **DNS 区域**"。 在 "显示" 窗格中，右键单击要为其更改访问作用域的 DNS 区域，然后单击 "**设置访问作用域**"。

    ![设置访问作用域](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)

3.  "**设置访问作用域**" 对话框将打开。 如果你的部署需要，请单击以取消选择 "**从父级继承访问作用域**"。 在 "**选择访问作用域**" 中，选择一个项目，然后单击 **"确定"**。

    ![选择访问作用域](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)

4.  在 "IPAM 客户端控制台显示" 窗格中，验证是否更改了区域的访问作用域。

    ![验证是否更改了区域的访问作用域](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)

## <a name="see-also"></a>另请参阅
[基于角色的访问控制](Role-based-Access-Control.md) 
[管理 IPAM](Manage-IPAM.md)



