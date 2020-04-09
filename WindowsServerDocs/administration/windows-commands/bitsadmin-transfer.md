---
title: bitsadmin Transfer
description: 用于传输一个或多个文件的 bitsadmin 传输的 Windows 命令主题。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e960b4d94416d57e6c42ec27057dafef5e44516
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849000"
---
# <a name="bitsadmin-transfer"></a>bitsadmin Transfer

传输一个或多个文件。 若要传输多个文件，请指定多个 \<RemoteFileName\>-\<LocalFileName\> 对。 对以空格分隔。

## <a name="syntax"></a>语法

```
bitsadmin /Transfer <Name> [<Type>] [/Priority <Job_Priority>] [/ACLFlags <Flags>] [/DYNAMIC] <RemoteFileName> <LocalFileName>
```

### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|名称|作业的名称。 与大多数命令不同，**名称**只能是名称而不是 GUID。|
|类型|可选-指定作业的类型。 将 **/DOWNLOAD** （默认值）用于下载作业或 **/UPLOAD**用于上载作业。|
|Priority|可选-将 job_priority 设置为以下值之一：</br>-前景</br>-高</br>-正常</br>-低|
|ACLFlags|可选-指示你希望在要下载的文件中维护所有者和 ACL 信息。 例如，若要维护文件的所有者和组，请将标志设置为 `OG`。 指定以下一个或多个标志：</br>-O：将所有者信息复制到文件。</br>-G：用文件复制组信息。</br>-D：将 DACL 信息复制到文件。</br>-S：复制具有文件的 SACL 信息。|
|/DYNAMIC|将作业配置[**BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](/windows/desktop/api/bits5_0/ne-bits5_0-bits_job_property_id)，放宽服务器端要求。|
|RemoteFileName|传输到服务器时文件的名称。|
|LocalFileName|位于本地的文件的名称。|

## <a name="remarks"></a>备注

默认情况下，BITSAdmin 服务创建一个按**正常**优先级运行的下载作业，并在传输完成之前或发生严重错误之前，用进度信息更新命令窗口。 如果作业成功传输所有文件并在发生严重错误时取消作业，则该服务将完成该作业。 如果该服务无法将文件添加到作业中，或者为*类型*或*Job_Priority*指定了无效的值，则该服务不会创建作业。 若要传输多个文件，请指定多个*RemoteFileName*-*LocalFileName*对。 对以空格分隔。

> [!NOTE]
> 如果发生暂时性错误，BITSAdmin 命令将继续运行。 若要结束命令，请按 CTRL + C。

## <a name="examples"></a><a name=BKMK_examples></a>示例

下面的示例启动一个名为*myDownloadJob*的传输作业。
```
C:\>bitsadmin /Transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)