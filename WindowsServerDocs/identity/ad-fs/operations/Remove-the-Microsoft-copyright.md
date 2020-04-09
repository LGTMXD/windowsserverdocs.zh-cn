---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: 删除 Microsoft 版权
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9306950ab83ea94c1ff814ea9a404c0efeff0e40
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816210"
---
# <a name="remove-the-microsoft-copyright"></a>删除 Microsoft 版权 


 
默认情况下，AD FS 页面包含 Microsoft 版权。 若要从自定义页面删除此版权，可以使用以下过程。 

![删除版权](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>删除 Microsoft 版权  
  
1. 创建基于默认主题的自定义主题。

   ```powershell
   New-AdfsWebTheme –Name custom –SourceName default
   ```

2. 通过指定输出文件夹来导出该主题。  

   ```powershell
   Export-AdfsWebTheme -Name custom -DirectoryPath C:\CustomWebTheme
   ```

3. 找到位于输出文件夹中的 `Style.css` 文件。 通过使用前面的示例，路径将为 `C:\CustomWebTheme\Css\Style.css.`
  
4. 使用编辑器（如记事本）打开 `Style.css` 文件。  
  
5. 找到 `#copyright` 部分，然后将其更改为以下内容：  

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. 创建基于新的 `Style.css` 文件的自定义主题。  

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. 激活新主题。  

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

现在，你应该不会再看到登录页面底部的版权。

![删除版权](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>其他参考 
[AD FS 用户登录自定义](AD-FS-user-sign-in-customization.md) 
