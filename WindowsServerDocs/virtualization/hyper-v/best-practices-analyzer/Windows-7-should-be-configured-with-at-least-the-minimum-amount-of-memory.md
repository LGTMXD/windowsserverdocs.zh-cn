---
title: 应至少为 Windows 7 配置最小内存量
description: 提供有关如何解决此最佳做法分析器规则报告的问题的说明。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 1b81ec0b-ceca-4fba-83ea-90d5f1d9bda8
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: c85b4c34141cecab842f76ea37add32fd4200b0b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992636"
---
# <a name="windows-7-should-be-configured-with-at-least-the-minimum-amount-of-memory"></a>应至少为 Windows 7 配置最小内存量

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[最佳做法分析器](https://go.microsoft.com/fwlink/?LinkId=122786)。

|属性|详细信息|
|-|-|
|**操作系统**|Windows Server 2016|
|**产品/功能**|Hyper-V|
|**严重性**|错误|
|**类别**|配置|

在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。

## <a name="issue"></a>问题

*将运行 Windows 7 的虚拟机配置为小于最小 RAM 量，即 512 MB。*

## <a name="impact"></a>影响

*以下虚拟机上的来宾操作系统可能无法运行或可能运行 unreliably：*
```
<list of virtual machine names>
```
## <a name="resolution"></a>解决方法

*使用 Hyper-v 管理器将分配给此虚拟机的内存增加到至少 512 MB。*

### <a name="to-increase-the-memory-using-hyper-v-manager"></a>使用 Hyper-v 管理器增加内存

1.  打开 Hyper-V 管理器。 单击 **“开始”**，指向 **“管理工具”**，然后单击 **“Hyper-V 管理器”**。

2.  在结果窗格中的 "**虚拟机**" 下，选择要配置的虚拟机。 虚拟机的状态应列为 "**关**"。 如果不是，请右键单击该虚拟机，然后单击 "**关闭**"。

3.  在 **“操作”** 窗格中的虚拟机名称下，单击 **“设置”**。

4.  在导航窗格中，单击 "**内存**"。

5.  在 "**内存**" 页上，将 "**启动 RAM** " 设置为至少 512 MB，然后单击 **"确定"**。

### <a name="increase-the-memory-using-windows-powershell"></a>使用 Windows PowerShell 增加内存

1.  打开 Windows PowerShell。 从桌面 (，单击 "**开始**"，然后开始键入**Windows PowerShell**。 ) 

2.  右键单击 " **Windows PowerShell** "，然后单击 "**以管理员身份运行**"。

3.  \<MyVM>将替换为虚拟机的名称后，运行此命令：

```
Set-VMMemory <MyVM> -StartupBytes 512MB
```

## <a name="see-also"></a>另请参阅
[Set-vmmemory](/powershell/module/hyper-v/set-vmmemory?view=win10-ps)