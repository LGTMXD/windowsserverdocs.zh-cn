---
title: 限制 Web 访问
description: 了解如何在 MultiPoint Services 中限制用户对 Internet 的访问权限
ms.date: 07/08/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 044f2fd5-5b87-42bb-ba0d-c06516ac48c8
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 485c82284df4d77eea075d092fa08c820567f6c3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853680"
---
# <a name="limit-web-access"></a>限制 Web 访问
除了监视单个桌面上的用户活动，作为管理用户，你还可以通过指示要阻止用户访问的允许网站和网站，限制用户对指定网站的访问权限。  
  
## <a name="to-limit-web-access-on-a-station"></a>在工作站上限制 Web 访问  
  
1. 在 MultiPoint 仪表板中的 " **Web 限制**" 选项卡上，单击 "**配置**"。 **配置 Web 限制**页将打开。 列出了用户可以访问的站点。  
  
2. 单击要在其上限制 Web 访问的用户工作站的缩略图。  
  
3. 在**选定项任务**之下，单击**在此工作站上限制 Web 访问**。 **配置 Web 限制**页将打开。 列出了用户可以访问的站点。  
  
4. 若要添加允许的站点，请键入 Web 地址，然后单击**添加**。  
  
   > [!NOTE]
   > 例如，输入 "Contoso.com" 允许或阻止相对于 www\.contoso.com 的站点（例如，www\.newpage.contoso.com）。 输入 "Contoso" 将允许或限制与 Contoso 相关的所有站点（包括 contoso.com、contoso.uk，等等）。  
  
5. 若要从允许的站点列表中删除 Web 地址，请单击要删除对其访问权限的 Web 地址，然后单击**删除**。  
  
## <a name="to-limit-web-access-on-all-stations"></a>在所有工作站上限制 Web 访问  
  
1. 在 MultiPoint 仪表板中的 " **Web 限制**" 选项卡上，单击 "开始"\-向下菜单，然后单击 "**限制所有桌面上的 Web 访问**"。  
  
   **配置 Web 限制**页将打开。 列出了用户可以访问的站点。 执行以下操作之一：  
  
2. 若要添加允许的站点，请单击**仅允许这些站点**，键入允许的 Web 地址，然后单击**添加**。  
  
   若要添加不希望用户访问的站点，请单击 "**仅禁止这些网站**"，键入不希望用户访问的 web 地址，然后单击 "**添加**"。  
  
   > [!NOTE]
   > 例如，输入 "Contoso.com" 允许或阻止相对于 www.contoso.com 的站点（例如，www\.newpage.contoso.com）。 输入 "Contoso" 将允许或限制与 Contoso 相关的所有站点（包括 contoso.com、contoso.uk，等等）。  
  
3. 若要从允许或禁止的站点列表中删除 Web 地址，请单击该 Web 地址，然后单击**删除**。  
  
## <a name="see-also"></a>另请参阅  
[管理用户桌面](manage-user-desktops-using-multipoint-dashboard.md)  
