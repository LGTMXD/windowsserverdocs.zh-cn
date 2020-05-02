---
title: extend
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2414e21d-fc0b-40e8-9e33-3e072f8ad76b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c5dfeeaec966bfab3c1de2bb91bf79c9d870401
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725664"
---
# <a name="extend"></a>extend

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

将焦点及其文件系统的卷或分区扩展到磁盘上\(的\)可用未分配空间。  
  
  
  
## <a name="syntax"></a>语法  
  
```  
extend [size=<n>] [disk=<n>] [noerr]  
extend filesystem [noerr]  
```  
  
### <a name="parameters"></a>参数  
  
| 参数  |                                                                                             描述                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 规格\=<n>  |      指定\)要添加到当前卷或\(分区的空间量（以 mb 为单位）。 如果没有给定大小，则使用磁盘上可用的所有连续可用空间。       |
| 磁盘\=<n>  |                          指定扩展卷或分区的磁盘。 如果未指定磁盘，则在当前磁盘上扩展卷或分区。                          |
| 文件系统 |                                   扩展具有焦点的卷的文件系统。 仅适用于未使用卷进行扩展的文件系统。                                    |
|   noerr    | 仅用于脚本编写。 出现错误时，DiskPart 继续处理命令，就像未发生错误一样。 如果没有此参数，则错误会导致 DiskPart 退出并出现错误代码。 |
  
## <a name="remarks"></a>备注  
  
-   在基本磁盘上，可用空间必须与具有焦点的卷或分区位于同一磁盘上。 它还必须紧跟在包含焦点\(的卷或分区之后，必须从下一个扇区偏移量\)开始。  
  
-   在具有简单卷或跨区卷的动态磁盘上，可以将卷扩展到任何动态磁盘上的任何可用空间。 使用此命令，可以将简单动态卷转换为跨区动态卷。 镜像、RAID\-5 和带区卷不能扩展。  
  
-   如果以前用 NTFS 文件系统格式化分区，则文件系统会自动扩展以填充更大的分区，并且不会丢失数据。  
  
-   如果以前使用 NTFS 以外的文件系统格式化分区，则该命令将失败，并且不会更改分区。  
  
-   如果先前未使用文件系统格式化分区，则仍将扩展该分区。  
  
-   分区必须具有关联的卷，然后才能对其进行扩展。  
  
## <a name="examples"></a>示例  
若要通过 500 mb 扩展包含焦点的卷或分区，请键入：  
  
```  
extend size=500 disk=3  
```  
  
若要在扩展卷后扩展其文件系统，请键入：  
  
```  
extend filesystem  
```  
  
## <a name="additional-references"></a>其他参考  
- [命令行语法项](command-line-syntax-key.md)  
  

  

