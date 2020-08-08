---
title: SMB-应打开文件和打印机共享端口
ms.date: 07/02/2012
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: dc2e1d7f5408ad123297b8df2dc06f59053fe870
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954764"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB：文件和打印机共享端口应打开


更新日期：2011年2月2日

适用于： Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，windows server 2012，Windows Server 2008 R2

*本主题旨在解决最佳做法分析器扫描标识的特定问题。只应将本主题中的信息应用到运行文件服务最佳做法分析器的计算机，并遇到本主题中所述的问题。有关最佳做法和扫描的详细信息，请参阅*[最佳做法分析器](https://go.microsoft.com/fwlink/?linkid=122786%0d%0a)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>操作系统</strong></p></td>
<td><p>Windows Server</p></td>
</tr>
<tr class="even">
<td><p><strong>产品/功能</strong></p></td>
<td><p>文件服务</p></td>
</tr>
<tr class="odd">
<td><p><strong>严重性</strong></p></td>
<td><p>错误</p></td>
</tr>
<tr class="even">
<td><p><strong>类别</strong></p></td>
<td><p>配置</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>问题

> * (端口445和 139) ，无法打开文件和打印机共享所需的防火墙端口。*

## <a name="impact"></a>影响

> *计算机将无法访问此服务器上的共享文件夹和其他服务器消息块 (基于 SMB) 的网络服务。*

## <a name="resolution"></a>解决方法

> *启用文件和打印机共享以便通过计算机的防火墙进行通信。*

**Administrators** 组中的成员身份或等效身份是完成此过程所需的最低要求。

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>打开防火墙端口以启用文件和打印机共享

1.  打开 "控制面板"，单击 "**系统和安全**"，然后单击 " **Windows 防火墙**"。

2.  在左窗格中，单击 "**高级设置**"，然后在控制台树中单击 "**入站规则**"。

3.  在 "**入站规则**" 下，找到 "规则**文件和打印机共享" (") 中**的文件和打印机共享"，并在 **) 中查找 (SMB 的文件和打印机共享**。

4.  请依次右键单击每个规则，然后单击“启用规则”。

## <a name="additional-references"></a>其他参考

[了解共享文件夹和 Windows 防火墙](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731402(v=ws.11)) (https://technet.microsoft.com/library/cc731402.aspx)
