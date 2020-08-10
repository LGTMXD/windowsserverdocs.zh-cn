---
title: 更改驱动器号
description: 如何使用磁盘管理在 Windows 中更改或分配驱动器号。
ms.date: 06/08/2020
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 52665f239bec56ad81d0300ed3312ec57b32cb1f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936068"
---
# <a name="change-a-drive-letter"></a>更改驱动器号

> **适用于：** Windows 10、Windows 8.1、Windows 7、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

如果你不喜欢某个驱动器的驱动器号，或者某个驱动器尚未分配驱动器号，可以使用磁盘管理来更改或分配驱动器号。 若要改为将驱动器装载到空文件夹，从而使其显示为文件夹，请参阅[将驱动器安装在文件夹中](assign-a-mount-point-folder-path-to-a-drive.md)。

> [!IMPORTANT]
> 如果更改驱动器号的驱动器中安装了 Windows 或应用，在运行或查找该驱动器时，应用可能会遇到问题。 出于此原因，我们建议不要更改安装了 Windows 或应用的驱动器的驱动器号。

下面是更改驱动器号的方法：

1. 使用管理员权限打开磁盘管理。
    为此，选择并按住（或右键单击）“开始”按钮，然后选择“磁盘管理”。
1. 在“磁盘管理”中，选择并按住（或右键单击）要更改或添加驱动器号的卷，然后选择“更改驱动器号和路径”。

    ![显示了驱动器的磁盘管理](media/change-drive-letter.png)
    > [!TIP]
    > 如果“更改驱动器号和路径”选项未显示或灰显，则可能表示该卷尚未准备好设置驱动器号。如果驱动器尚未分配并需要[初始化](initialize-new-disks.md)，则可能会出现这种情况。 或者，可能表示该卷不可访问。EFI 系统分区和恢复分区存在这种情况。 如果确认已使用可访问的驱动器号格式化了该卷，但依旧无法更改它，则很遗憾，本主题可能帮不到你，我们建议[联系 Microsoft](https://support.microsoft.com/contactus/) 或电脑制造商来获得更多帮助。

1. 若要更改驱动器号，请选择“更改”。 若要添加驱动器号（如果驱动器没有驱动器号），请选择“添加”。

    ![“更改驱动器号和路径”对话框](media/change-drive-letter2.png)
1. 选择新的驱动器号，选择“确定”，然后在出现有关依赖于该驱动器号的程序可能无法正常运行的提示时选择“是”。 

    ![显示更改驱动器号的“更改驱动器号和路径”对话框](media/change-drive-letter3.png)
