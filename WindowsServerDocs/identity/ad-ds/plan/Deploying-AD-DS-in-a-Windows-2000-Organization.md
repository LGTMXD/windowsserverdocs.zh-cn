---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: 在 Windows Server 2000 组织中部署 AD DS
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f1543effdb1cd9b83c0a2016855c4c65e3b2b5c0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822630"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>在 Windows Server 2000 组织中部署 AD DS

>适用于：Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

如果你的组织当前正在运行 Windows 2000 Active Directory，你可以通过执行将部分或全部域控制器的操作系统就地升级到 Windows Server 2008 或引入环境中运行 Windows Server 2008 的域控制器来部署 Windows Server 2008 Active Directory 域服务（AD DS）。  
  
在将运行 Windows Server 2008 的域控制器添加到现有 Windows 2000 Active Directory 域之前，必须运行**adprep**，这是一个命令行工具。 Adprep 扩展了 AD DS 架构，更新了所选对象的默认安全描述符，并添加了某些应用程序所需的新目录对象。 Windows Server 2008 安装磁盘（\sources\adprep\adprep.exe）上提供了 Adprep。 有关详细信息，请参阅 Adprep （[https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)）。  
  
> [!NOTE]  
> 如果要将现有 Windows 2000 AD DS 域控制器就地升级到 Windows Server 2008，则必须首先将服务器升级到 Windows Server 2003，然后将其升级到 Windows Server 2008。  
  
下图显示了在当前运行 Windows 2000 Active Directory 的网络环境中部署 Windows Server 2008 AD DS 的步骤。  
  
![在 windows 2000 组织中部署](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)  
  
> [!NOTE]  
> 如果要将域或林功能级别设置为 Windows Server 2008，环境中的所有域控制器都必须运行 Windows Server 2008 操作系统。  
  
将从 Windows 2000 环境就地升级的资源和帐户域合并为 Windows Server 2008 AD DS 部署的一部分可能需要林间或林内域重构。 在林之间重新构建 AD DS 域有助于降低组织的复杂性和相关的管理成本。 重构林中 AD DS 域可减少复制流量，减少所需的用户和组管理量，并简化组策略的管理，从而帮助你降低组织的管理开销。 有关详细信息，请参阅 ADMT 3.1 迁移指南（[https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)）。  
  
有关可用于在当前运行 Windows 2000 Active Directory 的组织中计划和部署 AD DS 的详细任务的列表，请参阅[清单：在 Windows 2000 组织中部署 AD DS](https://technet.microsoft.com/library/cc732737.aspx)。  
  


