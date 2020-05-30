---
title: pnpunattend
description: 了解如何在计算机上审核设备驱动程序，以及如何执行无提示的驱动程序安装。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: e79dd4869a88dc48e579451bfdf2f8fecc55e4f9
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222029"
---
# <a name="pnpunattend"></a>pnpunattend

审核计算机上的设备驱动程序，执行无人参与的驱动程序安装，或者在不安装的情况下搜索驱动程序，还可以在命令行中报告结果。 使用此命令为特定硬件设备指定特定驱动程序的安装。 请参阅“备注”。

## <a name="syntax"></a>语法

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|auditSystem|指定联机驱动程序安装。</br>必需，但在运行**pnpunattend**时，无论是 **/help**还是 **/？** 个参数。|
|/s|可选。 指定在不安装的情况下搜索驱动程序。|
|/L|可选。 指定在命令提示符中显示此命令的日志信息。|
|/?|可选。 在命令提示符下显示此命令的帮助。|

## <a name="remarks"></a>备注

需要初步准备。 在使用此命令之前，必须完成以下任务：

1. 为要安装的驱动程序创建一个目录。 例如，在**C:\Drivers\Video**中为视频适配器驱动程序创建一个文件夹。
2. 下载并提取设备的驱动程序包。 将包含操作系统版本 INF 文件的子文件夹的内容复制到所创建的视频文件夹中的所有子文件夹。 例如，将视频驱动程序文件复制到 C:\Drivers\Video。
3. 将系统环境路径变量添加到步骤1中创建的文件夹。例如， **C:\Drivers\Video**。
4. 创建以下注册表项，然后为创建的**DriverPaths**键将**值数据**设置为**1**。
5. 对于 Windows®7导航注册表路径： **HKEY_LOCAL_Machine \Software\microsoft\windows NT\CurrentVersion \\ **，然后创建密钥： **UnattendSettings\PnPUnattend\DriverPaths \\ **
6. 对于 Windows Vista，导航到注册表路径： **HK_LM \Software\microsoft\windows NT\CurrentVersion \\ **，然后创建密钥 = **\UnattendSettings\PnPUnattend\DriverPaths**。

## <a name="examples"></a>示例

To 命令显示了如何使用**PNPUnattend**审核计算机的可能的驱动程序更新，然后将发现报告给命令提示符。

```
pnpunattend auditsystem /s /l
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)