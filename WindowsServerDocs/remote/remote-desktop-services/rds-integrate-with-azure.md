---
title: RDS - 与 Azure 服务集成
description: 了解如何将 RDS 集成到 Azure 部署中，以及将 Azure 集成到 RDS 部署中。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/18/2017
ms.topic: article
author: lizap
ms.openlocfilehash: 2c792a22608fe0e7ae826b27d6917202037559e4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "80855070"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>远程桌面服务 - 与 Azure 服务集成

Windows Server 2016 集合了通过远程桌面服务安全提供桌面和应用的强大功能，以及 Microsoft Azure 提供的灵活、可缩放的服务。 可以使用 Azure 服务部署 RDS，以帮助降低本地服务器的基础结构维护成本，通过 Azure 服务确保高可用性来提高稳定性，通过多重身份验证提高安全性，以及通过使用现有身份访问 RDS 中的资源来改善用户体验。

使用以下信息将 Azure 集成到远程桌面部署中：

- [了解如何将多重身份验证用于 RDS](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [将 Azure AD 域服务与 RDS 部署集成](rds-azure-adds.md)
- [使用 Azure AD 应用程序代理发布远程桌面](/azure/active-directory/application-proxy-publish-remote-desktop)

若要了解这些服务如何简化远程桌面部署的体系结构，请查看[具有独有 Azure PaaS 角色的 RDS 体系结构](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles)。