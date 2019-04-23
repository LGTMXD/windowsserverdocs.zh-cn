---
title: 使用 convert RiprepImage 命令
description: 'Windows 命令主题 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf5fffdedbc25ad97e9e96a84d3ff1bbdaf87b2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835048"
---
# <a name="using-the-convert-riprepimage-command"></a>使用 convert RiprepImage 命令



将现有的远程安装准备 (RIPrep) 映像转换为 Windows 映像 (.wim) 格式。

## <a name="syntax"></a>语法

```
WDSUTIL [Options] /Convert-RIPrepImage /FilePath:<File path and name>
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/InPlace]
         [/Overwrite:{Yes | No | Append}]
```

## <a name="parameters"></a>Parameters

|参数|描述|
|---------|-----------|
|/ FilePath:\<文件路径和名称 >|指定对应于 RIPrep 映像的.sif 文件的完整路径和文件名。 此文件通常称为 Riprep.sif 和 \Templates 包含 RIPrep 映像的文件夹的子文件夹中找到。|
|/DestinationImage|指定目标图像中，使用以下选项的设置。</br>-/FilePath:\<文件路径和名称 >-设置为新文件的完整文件路径。 例如：**C:\Temp\convert.wim**</br>-[/Name:\<名称 >]-设置图像的显示名称。 如果未不指定任何显示名称，将使用源映像的显示名称。</br>-[/ 说明：\<说明 >]-设置映像的说明。</br>-[/InPlace]-指定转换应采用原始 RIPrep 映像而不是默认行为将原始图像的副本的位置。</br>-[/Overwrite: {是 | 否 | Append}]-确定是否在指定的文件 **/DestinationImage**应覆盖选项，如果在 /FilePath 已存在具有该名称的现有文件。 **是**将覆盖现有文件。 **不**（默认值） 后，如果已存在具有相同名称的另一个文件发生错误。 **追加**预先存在的.wim 文件中的新映像作为附加所生成的图像。|

## <a name="BKMK_examples"></a>示例

若要将指定的 RIPrep.sif 图像转换为 RIPREP.wim，键入：
```
WDSUTIL /Convert-RiPrepImage /FilePath:"R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif" /DestinationImage
/FilePath:"C:\Temp\RIPREP.wim"
```
若要使用指定的名称和说明，将指定的 RIPrep.sif 图像转换为 RIPREP.wim 和覆盖它使用新的文件，如果文件已存在，请键入：
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:"\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif"
/DestinationImage /FilePath:"\\Server\Share\RIPREP.wim"
/Name:"WindowsXP image" /Description:"Converted RIPREP image of WindowsXP"
/Overwrite:Append
```

#### <a name="additional-references"></a>其他参考

[命令行语法解答](command-line-syntax-key.md)