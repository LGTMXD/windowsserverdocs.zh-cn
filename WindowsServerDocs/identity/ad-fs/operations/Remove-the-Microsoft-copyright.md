---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: 删除 Microsoft 版权
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ec7d9cb02508fc046ce3e8f0378e63c82eecca8d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949771"
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

3. 找到 `Style.css` 位于输出文件夹中的文件。 通过使用前面的示例，路径将为`C:\CustomWebTheme\Css\Style.css.`

4. `Style.css`使用编辑器（如记事本）打开该文件。

5. 找到 `#copyright` 部分，然后将其更改为以下内容：

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. 创建基于新文件的自定义主题 `Style.css` 。

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
