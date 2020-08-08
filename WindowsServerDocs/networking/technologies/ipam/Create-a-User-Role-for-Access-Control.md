---
title: 为访问控制创建用户角色
description: 本主题是 Windows Server 2016 中的 IP 地址管理 (IPAM) 管理指南的一部分。
manager: brianlic
ms.topic: article
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 92f0c1860858f2f888c6d78e890d4d75dbc6e696
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966474"
---
# <a name="create-a-user-role-for-access-control"></a>为访问控制创建用户角色

>适用于：Windows Server（半年频道）、Windows Server 2016

你可以使用本主题在 IPAM 客户端控制台中创建新的访问控制用户角色。

Administrators**** 组成员或同等身份是执行此过程的最低要求。

> [!NOTE]
> 创建角色后，可以创建一个访问策略，将角色分配给特定用户或 Active Directory 组。 有关详细信息，请参阅[创建访问策略](../../technologies/ipam/Create-an-Access-Policy.md)。

### <a name="to-create-a-role"></a>创建角色

1.  在服务器管理器中，单击 " **IPAM**"。 IPAM 客户端控制台随即出现。

2.  在导航窗格中，单击 "**访问控制**"，然后在下部导航窗格中单击 "**角色**"。

    ![访问控制角色](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)

3.  右键单击 "**角色**"，然后单击 "**添加用户角色**"。

    ![添加用户角色](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)

4.  此时将打开 "**添加或编辑角色**" 对话框。 在 "**名称**" 中，键入使角色功能清晰的角色的名称。 例如，如果你想要创建允许管理员管理 DNS SRV 资源记录的角色，则可以将角色命名为**IPAMSrv**。 如果需要，在 "**操作**" 中向下滚动以找到要为角色定义的操作的类型。 在此示例中，向下滚动到 " **DNS 资源记录管理操作**"。

    ![DNS 资源记录管理操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)

5.  展开 " **DNS 资源记录管理操作**"，然后找到 " **SRV 记录操作**"。

    ![SRV 记录操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)

6.  展开并选择 " **SRV 记录操作**"，然后单击 **"确定"**。

    ![选择 SRV 记录操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)

7.  在 IPAM 客户端控制台中，单击刚创建的角色。 在**详细信息视图中，** 将显示角色允许的操作。

    ![新角色详细信息](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)

## <a name="see-also"></a>另请参阅
[基于角色的访问控制](Role-based-Access-Control.md) 
[管理 IPAM](Manage-IPAM.md)



