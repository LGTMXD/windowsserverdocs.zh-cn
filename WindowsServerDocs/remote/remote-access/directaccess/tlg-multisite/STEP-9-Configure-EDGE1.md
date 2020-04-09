---
title: 步骤9配置 EDGE1
description: 本主题是测试实验室指南-演示适用于 Windows Server 2016 的 DirectAccess 多站点部署的一部分
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: f6e8d85b-de65-43b3-bf3e-ec84471a1fcc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a3f0b291890e294389b611527bd34d2ec8afa832
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861530"
---
# <a name="step-9-configure-edge1"></a>步骤9配置 EDGE1

>适用于：Windows Server（半年频道）、Windows Server 2016

在 EDGE1 服务器上执行以下过程：  
  
1. 在 EDGE1 上配置 DNS 服务器。 需要在 EDGE1 上的 corp2.corp.contoso.com 域中配置 DNS 服务器。  
  
2. 配置子网之间的路由。 配置 EDGE1 上的路由，以便在公司网络和2公司网络之间实现通信。  
  
## <a name="configure-the-dns-servers-on-edge1"></a><a name="IPv6"></a>在 EDGE1 上配置 DNS 服务器  
  
1.  在服务器管理器控制台中，单击 "**本地服务器**"，然后在 "**属性**" 区域中的 "**公司**网络" 旁边，单击链接。  
  
2.  在 "网络连接" 窗口中，右键单击 "**企业**网络"，然后单击 "**属性**"。  
  
3.  单击 **“Internet 协议版本 4 (TCP/IPv4)”** ，然后单击 **“属性”** 。  
  
4.  在 "**备用 DNS 服务器**" 中，键入**10.2.0.1**。 然后单击 **“确定”** 。  
  
5.  单击“Internet 协议版本 6 (TCP/IPv6)”，然后单击“属性”。  
  
6.  在 "**备用 DNS 服务器**" 中，键入 " **2001： db8：2：： 1** "，然后单击 **"确定"** 。  
  
7.  在 "**公司网络属性**" 对话框中，单击 "**关闭**"。  
  
8.  关闭 **“网络连接”** 窗口。  
  
## <a name="configure-routing-between-subnets"></a><a name="ConfigRouting"></a>配置子网之间的路由  
  
1.  在 "**开始**" 屏幕上，键入**cmd.exe**，右键单击 " **Cmd**"，单击 "**高级**"，然后单击 "以**管理员身份运行**"。 如果出现了 **“用户帐户控制”** 对话框，请确认其中显示的操作为所需的操作，然后单击 **“是”** 。  
  
2.  在 "命令提示符" 窗口中，输入以下命令。 输入每个命令后，按 ENTER。  
  
    ```  
    netsh interface IPv4 add route 10.2.0.0/24 Corpnet 10.0.0.254  
    netsh interface IPv6 add route 2001:db8:2::/64 Corpnet 2001:db8:1::fe  
    ```  
  
3.  关闭“命令提示符”窗口。  
  


