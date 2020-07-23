---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: 方案访问-拒绝帮助
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2d3f0f7f0fa611ab34145aa35291ff9d07b0b205
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955949"
---
# <a name="scenario-access-denied-assistance"></a>方案：拒绝访问协助

>适用于：Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

当用户尝试访问其不具有访问权限的文件服务器上的共享文件和文件夹时，他们将收到一条拒绝访问的消息。 管理员通常不具有用于解决访问问题的相应上下文，这使他们难以解决该问题。  
  
## <a name="scenario-description"></a>方案描述  
"拒绝访问" 协助是 Windows Server 2012 中的一项新功能，它提供了以下方式来解决与访问文件和文件夹相关的问题：  
  
-   **自我协助。** 如果用户可以确定造成问题的原因并修正该问题，则该用户就可获得所请求的访问权限，这样可以降低对业务的影响，并且不需要在中心访问策略中设置特殊例外。 “拒绝访问”协助提供了一条拒绝访问的消息，文件服务器管理员可以使用特定于其组织的信息自定义该消息。 例如，管理员可以设置该消息，以便用户可以从数据所有者请求访问权限，而无需文件服务器管理员干预。  
  
-   **由数据所有者提供协助。** 你可以为共享文件夹定义通讯组列表并配置它，以便文件夹所有者可以在用户需要访问时收到电子邮件通知。 如果数据所有者不知道如何帮助用户获取访问权限，则该数据所有者可以将此信息转发给文件服务器管理员。  
  
-   **由文件服务器管理员提供协助。** 当用户不能解决问题且数据所有者无法提供帮助时，可提供这种类型的协助。  Windows Server 2012 提供了一个用户界面，文件服务器管理员可以在其中查看用户对文件或文件夹的有效权限，以便更轻松地排查访问问题。  
  
Windows Server 2012 中的 "拒绝访问" 协助为文件服务器管理员提供了相关访问详细信息，以便他们可以确定问题和相应的工具，以便他们能够进行配置更改以满足访问请求。 例如，用户可以按照以下步骤访问一个他们当前没有访问权限的文件：  
  
-   用户试图读取 \financeshares 共享文件夹中的文件 \\ ，但服务器显示拒绝访问的消息。  
  
-    Windows Server 2012 向用户显示 "拒绝访问" 协助信息，其中包含请求协助的选项。  
  
-   如果用户请求访问资源，则服务器会向文件夹所有者发送一封包含访问请求信息的电子邮件。  
  
可以在[“拒绝访问”协助规划](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)中找到关于配置“拒绝访问”协助的规划信息。  
  
你可以在[&#41;&#40;演示步骤](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)中找到有关配置 "拒绝访问" 协助的步骤。  
  
## <a name="in-this-scenario"></a>本方案内容  
本方案是动态访问控制方案的一部分。 有关动态访问控制的其他信息，请参阅：  
  
-   [动态访问控制：方案概述](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>实际的应用程序  
Windows Server 2012 中的 "拒绝访问" 协助使用户能够直接从拒绝访问消息请求对共享文件和文件夹的访问权限，从而有助于实现动态访问控制。  
  
## <a name="features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>本方案中所含的功能  
下表列出了本方案的部分功能并说明了支持该方案的工作原理。  
  
|功能|如何支持本方案|  
|-----------|---------------------------------|  
|[File Server Resource Manager Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11))|通过使用文件服务器上的文件服务器资源管理器控制台，可以配置“拒绝访问”协助。|  
|[文件和存储服务概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831487(v=ws.11))|文件服务器资源管理器是文件和存储服务的角色服务，并且它包含一组可用于管理你网络上的文件服务器的功能。|  
  
