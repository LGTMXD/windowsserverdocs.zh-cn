---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: AD FS 中的自定义 Web 主题
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 69255eeaecd3e5198054242c1ab6dd1d0a58ce33
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816420"
---
# <a name="custom-web-themes-in-ad-fs"></a>AD FS 中的自定义 Web 主题 

\-box\-\-提供的主题称为 "默认"。 可以导出并使用该默认主题，以便可以快速启动。 通过修改 .css 文件、导入和应用此新主题，你可以自定义外观和行为，包括布局，然后便可以使用自定义的外观和行为。 使用 .css 文件还会使 Web 设计人员的工作变得更容易。  
  
以下 cmdlet 创建了一个复制默认 Web 主题的自定义 Web 主题。  
  
  
`New-AdfsWebTheme –Name custom –SourceName default ` 

  
你可以修改 .css 文件，并通过使用新的 .css 文件来配置新的 Web 主题。 若要导出 Web 主题，请使用以下 cmdlet。  
  

    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  

  
若要将 .css 文件应用于新的主题，请使用以下 cmdlet。  
  

    Set-AdfsWebTheme –TargetName custom –StyleSheet @{path="c:\NewTheme.css"}  
  
  
以下 cmdlet 从新的样式表创建自定义 Web 主题。  
  
  
`New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"} –RTLStyleSheetPath c:\NewRtlTheme.css ` 
  
  
  
若要将自定义 web 主题应用到 AD FS，请使用以下 cmdlet。  
  

`Set-AdfsWebConfig -ActiveThemeName custom`  

  
若要将 JavaScript 添加到 AD FS，请使用以下 cmdlet。  
  
 
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=' /adfs/portal/script/onload.js';path="D:\inetpub\adfsassets\script\onload.js"}  


## <a name="additional-references"></a>其他参考 
[AD FS 用户登录自定义](AD-FS-user-sign-in-customization.md)  
