---
title: pwlauncher
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ddda3ab7831643c3c2c096ae87893d97f90155c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722755"
---
# <a name="pwlauncher"></a>pwlauncher



启用或禁用 Windows To 中转启动选项（pwlauncher）。 使用**pwlauncher**命令行工具，可以将计算机配置为自动启动到 Windows to 中转工作区（假设有），而无需输入固件或更改启动选项。



## <a name="syntax"></a>语法

```
Pwlauncher {/enable | /disable}
```

### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|/enable|启用 Windows To boot 选项，使计算机在出现时自动从 USB 设备启动|
|/disable|禁用 Windows To 中转启动选项，使计算机无法从 USB 设备启动，除非在固件中手动配置。|
|/?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注

如果用户想要使用 Windows To 中转，最大的障碍就是让他们的计算机从 USB 启动。 通常通过输入固件并尝试不同的配置选项来完成此操作，直到计算机配置正确为止。 对于大多数用户来说，这并不是一个简单的任务，因为固件包含的选项可能会导致系统无法使用（如果使用不正确）。 为了帮助缓解此问题，Windows 8and 更高版本的操作系统中包含一个名为 Windows To 中转启动选项的功能，该功能允许用户将其计算机配置为从 Windows 内部启动，而无需输入其固件，只要其固件支持从 USB 启动。 若要使系统始终从 USB 首次启动，则需要考虑一些问题。 例如，可能会无意中启动包含恶意软件的 USB 设备来危害系统，或插入多个 USB 驱动器，导致启动冲突。 出于此原因，默认配置将默认禁用 Windows To To Startup 选项。 此外，需要管理员特权才能配置 Windows To 中转启动选项。 如果使用 pwlauncher 命令行工具或 "**更改 Windows To To Boot 启动选项**" 应用程序启用 Windows to boot 启动选项，计算机将尝试从插入到计算机的任何 USB 设备启动，然后再启动该计算机。

## <a name="examples"></a>示例

若要演示如何使用**pwlauncher**命令启用从 USB 启动：
```
Pwlauncher /enable
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)