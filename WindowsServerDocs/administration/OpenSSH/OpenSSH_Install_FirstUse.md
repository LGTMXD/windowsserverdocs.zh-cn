---
title: 安装适用于 Windows Server 的 OpenSSH
description: 使用 Windows 设置选项或 Windows PowerShell 安装适用于 Windows Server 的 OpenSSH 客户端和服务器。
ms.date: 09/27/2019
ms.topic: conceptual
contributor: maertendMSFT
author: maertendmsft
ms.openlocfilehash: 8ed486adb9519fbc0f87cc3142386bec8211d783
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469782"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>安装适用于 Windows Server 2019 和 Windows 10 的 OpenSSH

在 Windows Server 2019 和 Windows 10 1809 中，OpenSSH 客户端和 OpenSSH 服务器是可单独安装的组件。
具有这些 Windows 版本的用户应使用以下说明来安装和配置 OpenSSH。

> [!NOTE]
> 从 PowerShell GitHub 存储库 (https://github.com/PowerShell/OpenSSH-Portable) 获取了 OpenSSH 的用户应当使用那里的说明，不应当使用这些说明。

## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>从 Windows Server 2019 或 Windows 10 1809 上的“设置”UI 安装 OpenSSH

OpenSSH 客户端和服务器是 Windows 10 1809 的可安装功能。

若要安装 OpenSSH，请启动“设置”，然后转到“应用”>“应用和功能”>“管理可选功能”。

扫描此列表，查看 OpenSSH 客户端是否已安装。 如果没有，则在页面顶部选择“添加功能”，然后：

* 若要安装 OpenSSH 客户端，请找到“OpenSSH 客户端”，然后单击“安装”。
* 若要安装 OpenSSH 服务器，请找到“OpenSSH 服务器”，然后单击“安装”。

安装完成后，请返回“应用”>“应用和功能”>“管理可选功能”，你应当会看到列出的 OpenSSH 组件。

> [!NOTE]
> 安装 OpenSSH 服务器将创建并启用名为“OpenSSH-Server-In-TCP”的防火墙规则。 这允许端口 22 上的入站 SSH 流量。

## <a name="installing-openssh-with-powershell"></a>通过 PowerShell 安装 OpenSSH

若要使用 PowerShell 安装 OpenSSH，请首先以管理员身份启动 PowerShell。
若要确保 OpenSSH 功能可以安装，请执行以下操作：

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

然后，安装服务器和/或客户端功能：

```powershell
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Both of these should return the following output:

Path          :
Online        : True
RestartNeeded : False
```

## <a name="uninstalling-openssh"></a>卸载 OpenSSH

若要使用 Windows“设置”卸载 OpenSSH，请启动“设置”，然后转到“应用”>“应用和功能”>“管理可选功能”。
在已安装功能的列表中，选择 OpenSSH 客户端或 OpenSSH 服务器组件，然后选择“卸载”。

若要使用 PowerShell 卸载 OpenSSH，请使用以下命令之一：

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

如果卸载 OpenSSH 时该服务正在使用中，则在删除后可能需要重启 Windows。


## <a name="initial-configuration-of-ssh-server"></a>SSH 服务器的初始配置

若要配置 OpenSSH 服务器以在 Windows 上首次使用，请以管理员身份启动 PowerShell，然后运行以下命令来启动 SSHD 服务：

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup.
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled
# If the firewall does not exist, create one
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

## <a name="initial-use-of-ssh"></a>首次使用 SSH

在 Windows 上安装 OpenSSH 服务器后，可以从安装了 SSH 客户端的任何 Windows 设备上使用 PowerShell 来快速测试它。
在 PowerShell 中，键入以下命令：

```powershell
Ssh username@servername
```

到任何服务器的第一个连接都将生成类似以下内容的消息：

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

回答必须是“yes”或“no”。
回答 Yes 会将该服务器添加到本地系统的已知 ssh 主机列表中。

系统此时会提示你输入密码。 作为安全预防措施，密码在键入的过程中不会显示。

在连接后，你将看到类似于以下内容的命令 shell 提示符：

```
domain\username@SERVERNAME C:\Users\username>
```

Windows OpenSSH 服务器使用的默认 shell 是 Windows 命令行解释器。

