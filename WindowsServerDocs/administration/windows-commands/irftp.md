---
title: irftp
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34f912878b97bd00fb1c4ea539c7ea4c1423ea59
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724817"
---
# <a name="irftp"></a>irftp

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

通过红外链接发送文件。    
## <a name="syntax"></a>语法  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

#### <a name="parameters"></a>参数  
|参数|描述|  
|-------|--------|  
|驱动器：\|指定包含要通过红外链接发送的文件的驱动器。|  
|通道名字|指定要通过红外链接发送的文件或文件集的位置和名称。 如果指定一组文件，则必须指定每个文件的完整路径。|  
|/h|指定隐藏模式。 当使用隐藏模式时，将在不显示 "无线链接" 对话框的情况下发送文件。|  
|/s|打开 "无线链接" 对话框，以便您可以选择要发送的文件或文件集，而无需使用命令行来指定驱动器、路径和文件名。|  

## <a name="remarks"></a>备注  
-   使用此命令之前，验证要通过红外链接进行通信的设备是否已启用红外线功能并正常工作，以及是否在设备之间建立了红外链接。  
-   如果在没有参数的情况下使用或与 **/s**一起使用，则**irftp**将打开 "**无线链接**" 对话框，你可以在其中选择要发送的文件，而无需使用命令行。  

## <a name="examples"></a>示例  
通过红外链接发送 Example .txt。  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>其他参考  
-   - [命令行语法项](command-line-syntax-key.md)  
