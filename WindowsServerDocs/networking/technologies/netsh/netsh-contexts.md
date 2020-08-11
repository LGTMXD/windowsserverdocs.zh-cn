---
title: Netsh 命令语法、上下文和格式设置
description: 你可以使用本主题来学习如何输入 netsh 上下文和子上下文、了解 netsh 语法和命令格式，以及如何在运行 Windows Server 2016 或 Windows 10 的本地和远程计算机上运行 netsh 命令。
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f72d3dfc3cd6f54b123cb00baf9ba75e4faeb906
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969464"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh 命令语法、上下文和格式设置

>适用于：Windows Server（半年频道）、Windows Server 2016

你可以使用本主题来学习如何输入 netsh 上下文和子上下文、了解 netsh 语法和命令格式，以及如何在本地和远程计算机上运行 netsh 命令。

Netsh 是命令行脚本实用工具，可让你显示或修改当前正在运行的计算机的网络配置。 可以通过在 netsh 提示符下键入命令来运行 Netsh 命令，并且可以在批处理文件或脚本中使用 Netsh 命令。 可以使用 netsh 命令来配置远程计算机和本地计算机。

Netsh 还提供脚本功能，可让你在批处理模式下对指定的计算机运行一组命令。 你可以使用 Netsh 将配置脚本保存在文本文件中，以便存档或者帮助你配置其他计算机。

## <a name="netsh-contexts"></a>Netsh 上下文

Netsh 使用动态\-链接库 \(DLL\) 文件与其他操作系统组件进行交互。

每个 netsh 帮助程序 DLL 提供一组称为“上下文”的广泛功能，这是一组特定于网络服务器角色或功能的命令  。 这些上下文通过为一个或多个服务、实用工具或协议提供配置和监视支持来扩展 netsh 的功能。 例如，Dhcpmon.dll 向 netsh 提供配置和管理 DHCP 服务器所需的上下文和命令集。

### <a name="obtain-a-list-of-contexts"></a>获取上下文列表

可以通过在运行 Windows Server 2016 或 Windows 10 的计算机上打开命令提示符或 Windows PowerShell 来获取 netsh 上下文列表。 键入命令 netsh，然后按 Enter  。 键入 /?，然后按 Enter  。

下面是运行 Windows Server 2016 Datacenter 的计算机上的这些命令的示例输出。

>    ```
>   PS C:\Windows\system32> netsh
>   netsh>/?
>
>    The following commands are available:
>
>    Commands in this context:
>    ..            - Goes up one context level.
>    ?             - Displays a list of commands.
>    abort         - Discards changes made while in offline mode.
>    add           - Adds a configuration entry to a list of entries.
>    advfirewall   - Changes to the `netsh advfirewall' context.
>    alias         - Adds an alias.
>    branchcache   - Changes to the `netsh branchcache' context.
>    bridge        - Changes to the `netsh bridge' context.
>    bye           - Exits the program.
>    commit        - Commits changes made while in offline mode.
>    delete        - Deletes a configuration entry from a list of entries.
>    dhcpclient    - Changes to the `netsh dhcpclient' context.
>    dnsclient     - Changes to the `netsh dnsclient' context.
>    dump          - Displays a configuration script.
>    exec          - Runs a script file.
>    exit          - Exits the program.
>    firewall      - Changes to the `netsh firewall' context.
>    help          - Displays a list of commands.
>    http          - Changes to the `netsh http' context.
>    interface     - Changes to the `netsh interface' context.
>    ipsec         - Changes to the `netsh ipsec' context.
>    ipsecdosprotection - Changes to the `netsh ipsecdosprotection' context.
>    lan           - Changes to the `netsh lan' context.
>    namespace     - Changes to the `netsh namespace' context.
>    netio         - Changes to the `netsh netio' context.
>    offline       - Sets the current mode to offline.
>    online        - Sets the current mode to online.
>    popd          - Pops a context from the stack.
>    pushd         - Pushes current context on stack.
>    quit          - Exits the program.
>    ras           - Changes to the `netsh ras' context.
>    rpc           - Changes to the `netsh rpc' context.
>    set           - Updates configuration settings.
>    show          - Displays information.
>    trace         - Changes to the `netsh trace' context.
>    unalias       - Deletes an alias.
>    wfp           - Changes to the `netsh wfp' context.
>    winhttp       - Changes to the `netsh winhttp' context.
>    winsock       - Changes to the `netsh winsock' context.
>
>    The following sub-contexts are available:
>     advfirewall branchcache bridge dhcpclient dnsclient firewall http interface ipsec ipsecdosprotection lan namespace netio ras rpc trace wfp winhttp winsock
>
>    To view help for a command, type the command, followed by a space, and then type ?.
>    ```

### <a name="subcontexts"></a>子上下文

Netsh 上下文可以同时包含命令和其他上下文（称为“子上下文”  ）。 例如，在 Routing 上下文中可以更改为 IP 和 IPv6 子上下文。

若要显示可在上下文中使用的命令和子上下文列表，请在 netsh 提示符下键入上下文名称，然后键入 /?  或 help  。 例如，若要显示可以在 Routing 上下文中使用的子上下文和命令的列表，请在 netsh 提示符 \(即 netsh&gt;\) 中，键入以下命令之一  ：

routing /? 

routing help 

若要在不更改当前上下文的情况下在另一个上下文中执行任务，请在 netsh 提示符下键入要使用的命令的上下文路径。 例如，若要在 IGMP 上下文中添加名为“Local Area Connection”的接口，且无需提前更改为 IGMP 上下文，请在 netsh 提示符下键入：

routing ip igmp add interface "Local Area Connection" startupqueryinterval=21 

## <a name="running-netsh-commands"></a>运行 netsh 命令

若要运行 netsh 命令，则必须在命令提示符下键入 netsh，然后按 Enter 以启动 netsh  。 接下来可以更改为包含要使用的命令的上下文。 可用的上下文取决于已安装的网络组件。 例如，如果在 netsh 提示符下键入 dhcp 并按 Enter，则 netsh 将更改为 DHCP 服务器上下文  。 但如果未安装 DHCP，则会显示以下消息：

找不到以下命令：dhcp  。

## <a name="formatting-legend"></a>格式设置图例

当在 netsh 提示符下或在批处理文件或脚本中运行命令时，可以使用以下格式设置图例来解释和使用正确的 netsh 命令语法。

- 斜体文本是键入命令时必须提供的信息  。 例如，如果命令有一个名为 -*UserName* 的参数，则必须键入实际的用户名。
- 粗体文本是键入命令时必须完全按所示内容键入的信息  。
- 后跟省略号 \(…\) 的文本是可在命令行中重复多次的参数。
- 方括号 [&nbsp;] 中间的文本是可选项。
- 大括号 {&nbsp;} 中间用竖线分隔的选项文本提供了一组选项，你只能从中选择一个选项，如 `{enable|disable}`。
- 字体格式为 Courier 的文本是代码或程序输出。

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>在命令提示符或 Windows PowerShell 中运行 Netsh 命令

若要在命令提示符处或在 Windows PowerShell 中启动 Network Shell 并输入 netsh，可以使用以下命令。

### <a name="netsh"></a>netsh

Netsh 是命令行脚本实用工具，可让你以本地或远程方式显示或修改当前正在运行的计算机的网络配置。 当不配合参数使用时，netsh 会打开 Netsh.exe 命令提示符 \(即 netsh&gt;\)   。

#### <a name="syntax"></a>语法

**netsh**\[ **-a**&nbsp;*AliasFile*\] \[ **-c**&nbsp;*Context* \] \[ **-r**&nbsp;*RemoteComputer*\] \[ **-u** \[ *DomainName\\* \] *UserName* \] \[ **-p**&nbsp;*Password* | \*\] \[{*NetshCommand* |  **-f**&nbsp;*ScriptFile*}\]

##### <a name="parameters"></a>参数

**`-a`**

可选。 指定在运行 AliasFile 后，返回到 netsh 提示符   。

**`AliasFile`**

可选。 指定包含一个或多个 netsh 命令的文本文件的名称  。

**`-c`**

可选。 指定 netsh 输入指定的 netsh 上下文  。

**`Context`**

可选。 指定要输入的 netsh 上下文  。

**`-r`**

可选。 指定希望命令在远程计算机上运行。

> [!IMPORTANT]
> 使用在另一台计算机上远程将某些 netsh 命令与 netsh –r 参数配合使用时，远程注册表服务必须在远程计算机上运行  。 如果未运行，Windows 将显示“找不到网络路径”错误消息。

***`RemoteComputer`***

可选。 指定要配置的远程计算机。

**`-u`**

可选。 指定要在用户帐户下运行 netsh 命令。

***`DomainName\\`***

可选。 指定用户帐户所在的域。 如果未指定 DomainName\\，则默认值为本地域  。

***`UserName`***

可选。 制定用户帐户名称。

**`-p`**

可选。 指定要为该用户帐户提供密码。

***`Password`***

可选。 为使用 -u UserName 指定的用户帐户指定密码   。

***`NetshCommand`***

可选。 指定要运行的 netsh 命令  。

**`-f`**

可选。 运行用 ScriptFile 指定的脚本之后退出 netsh   。

***`ScriptFile`***

可选。 指定要运行的脚本。

**`/?`**

可选。 在 netsh 提示符下显示帮助。

> [!NOTE]
> 如果指定 `-r` 后跟另一个命令，netsh 会在远程计算机上运行该命令，然后返回到 Cmd.exe 命令提示符   。 如果指定 `-r` 不包含其他命令，则 netsh 在远程模式下打开   。 此过程类似于在 Netsh 命令提示符下使用 set machine  。 使用 `-r` 时，仅为 netsh 的当前实例设置目标计算机   。 退出并重新输入 netsh 后，目标计算机将重置为本地计算机  。 通过指定存储在 WINS 中的计算机名称、UNC 名称、DNS 服务器要解析的 Internet 名称或 IP 地址，可以在远程计算机上运行 netsh 命令  。

**键入 netsh 命令的参数字符串值**

在 Netsh 命令引用中，有些命令包含需要字符串值的参数。

如果字符串值在字符之间包含空格（例如，包含多个单词的字符串值），则需要将字符串值括在引号中。 例如，如果一个名为 interface 的参数的字符串值为 Wireless Network Connection，请使用引号将字符串值括起来   ：

**`interface="Wireless Network Connection"`**

