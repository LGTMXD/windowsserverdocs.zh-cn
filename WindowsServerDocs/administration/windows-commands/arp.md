---
title: arp
description: 用于**arp**的 Windows 命令主题，用于显示和修改用于存储 IP 地址的地址解析协议（arp）缓存中的条目，以及它们的已解析物理地址。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 289ab87c99512c7c34154d4b85d541db82ab296b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851310"
---
# <a name="arp"></a>arp

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

显示和修改地址解析协议（ARP）缓存中的条目。 ARP 缓存包含一个或多个用于存储 IP 地址及其解析的以太网或令牌环物理地址的表。 计算机上安装的每个以太网或令牌环网络适配器都有一个单独的表。 在没有参数的情况下使用， **arp**显示帮助信息。

## <a name="syntax"></a>语法
```
arp [/a [<Inetaddr>] [/n <ifaceaddr>]] [/g [<Inetaddr>] [-n <ifaceaddr>]] [/d <Inetaddr> [<ifaceaddr>]] [/s <Inetaddr> <Etheraddr> [<ifaceaddr>]]
```
#### <a name="parameters"></a>参数

| 参数 | 说明 |
| --------- | ----------- |
| `/a [<Inetaddr>] [/n <ifaceaddr>]` | 显示所有接口的当前 arp 缓存表。 `/n` 参数区分大小写。 若要显示特定 IP 地址的 arp 缓存条目，请将**arp/a**与*Inetaddr*参数一起使用，其中*Inetaddr*是一个 IP 地址。 如果未指定*Inetaddr* ，则使用第一个适用的接口。 若要显示特定接口的 arp 缓存表，请结合 **/a**参数使用 * */n * * * ifaceaddr*参数，其中*ifaceaddr*是分配给接口的 IP 地址。 |
| `/g [<Inetaddr>] [/n <ifaceaddr> `] | 与 **/a**相同。 |
|`[/d <Inetaddr> [<ifaceaddr>]` | 删除具有特定 IP 地址的条目，其中*Inetaddr*是 ip 地址。 若要删除表中特定接口的条目，请使用*ifaceaddr*参数，其中*ifaceaddr*是分配给接口的 IP 地址。 若要删除所有条目，请使用星号（\*）通配符替代*Inetaddr*。 |
|`/s <Inetaddr> <Etheraddr> [<ifaceaddr>]` | 将一个静态条目添加到 arp 缓存，将 IP 地址*Inetaddr*解析为物理地址*Etheraddr*。 若要为特定接口将静态 arp 缓存条目添加到表中，请使用*ifaceaddr*参数，其中*ifaceaddr*是分配给接口的 IP 地址。 |
|`/?`| 在命令提示符下显示帮助。 |

## <a name="remarks"></a>备注
- *Inetaddr*和*ifaceaddr*的 IP 地址以点分隔的十进制表示法表示。
- *Etheraddr*的物理地址包含六个用十六进制表示法表示并由连字符分隔的字节（例如，00-AA-00-4F-9C）。

- 用 **/s**参数添加的条目是静态的，不会在 arp 缓存中超时。 如果已停止并启动 TCP/IP 协议，则会删除这些条目。 若要创建永久静态 arp 缓存条目，请将相应的**arp**命令放在批处理文件中，并使用计划任务在启动时运行批处理文件。

## <a name="examples"></a><a name=BKMK_Examples></a>示例

若要显示所有接口的 arp 缓存表，请键入：

```
arp /a
```

若要为分配了 IP 地址10.0.0.99 的接口显示 arp 缓存表，请键入：

```
arp /a /n 10.0.0.99
```

若要添加将 IP 地址10.0.0.80 解析为物理地址 00-AA-4F-9C 的静态 arp 缓存项，请键入：

```
arp /s 10.0.0.80 00-AA-00-4F-2A-9C 
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)
