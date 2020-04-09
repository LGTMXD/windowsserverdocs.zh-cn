---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: 群集感知更新插件的工作原理
description: 当使用 Windows Server 中的群集感知更新在群集上安装更新时，如何使用插件协调更新。
ms.topic: article
ms.prod: windows-server
manager: lizross
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
ms.openlocfilehash: ac37e4e7cc18da0d837e9c078382e59415c0edaf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828030"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>群集感知更新插件的工作原理

>适用于： Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

[群集感知更新](cluster-aware-updating.md)（CAU）使用插件跨故障转移群集中的节点协调更新的安装。 本主题提供有关使用 CAU 插件\-中的内置\-或为 CAU 安装的其他插件\-的信息。

## <a name="install-a-plug-in"></a><a name="BKMK_INSTALL"></a>安装插件\-  
除了使用 CAU \(**microsoft.windowsupdateplugin**和**microsoft.hotfixplugin**\) 安装的默认插件\-以外，还必须单独安装\-插件。 如果在自动\-更新模式中使用 CAU，则必须在所有群集节点上安装的插件\-。 如果在远程\-更新模式中使用 CAU，则中的插件\-必须安装在远程更新协调器计算机上。 你安装的插件\-可能会在每个节点上有其他安装要求。  
  
若要在中安装插件\-，请按照 publisher 中的插件\-中的说明进行操作。 若要使用 CAU 手动注册插件\-，请在安装了插件\-的每台计算机上运行[register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) cmdlet。  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>在参数中指定插件\-并将其插入\-  
  
### <a name="specify-a-cau-plug-in"></a>指定 CAU 插件\-

在 CAU UI 中，当你使用 CAU 来执行以下操作时，可以从可用插件\-的\-下拉列表中选择一个插件\-：  
  
-   将更新应用到群集  
  
-   群集的预览更新  
  
-   配置群集自我\-更新选项  
  
默认情况下，CAU 会选择**microsoft.windowsupdateplugin**中的插件\-。 不过，你可以指定中安装并注册了 CAU 的任何插件\-。

> [!TIP]  
> 在 CAU UI 中，你只能为 CAU 指定一个用于在更新运行期间用于预览或应用更新的插件\-。 通过使用 CAU PowerShell cmdlet，你可以指定一个或多个即插\-。如果需要在群集上安装多个类型的更新，则在一个更新运行中指定多个插件\-，而不是对中的每个插件\-使用单独的更新运行，这通常更有效。 例如，通常会发生更少的节点重新启动。

通过使用下表中列出的 CAU PowerShell cmdlet，可以通过传递 **– CauPluginName**参数指定一个或多个用于更新运行或扫描的插件\-。 可以在名称中指定多个即插\-，方法是使用逗号分隔这些名称。 如果指定多个插件\-，则还可以通过指定 **\-RunPluginsSerially**、 **\-StopOnPluginFailure**和 **– SeparateReboots**参数，控制插件\-在更新运行期间如何相互影响。 有关使用多个插件\-的详细信息，请使用下表中的 cmdlet 文档所提供的链接。  
  
|Cmdlet|说明|  
|----------|---------------|  
|[Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/add-cauclusterrole)|将提供自我\-更新功能的 CAU 群集角色添加到指定的群集。|  
|[Invoke-caurun](https://docs.microsoft.com/powershell/module/clusterawareupdating/invoke-caurun)|为适用的更新执行群集节点的扫描并通过更新运行在指定的群集上安装这些更新。|  
|[Invoke-causcan](https://docs.microsoft.com/powershell/module/clusterawareupdating/invoke-causcan)|为适用的更新执行群集节点的扫描，并返回将应用于指定群集中每个节点的更新的初始集列表。|  
|[Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/set-cauclusterrole)|为指定群集上的 CAU 群集角色设置配置属性。|  
  
如果未使用这些 cmdlet 指定 CAU 插件\-in 参数，则默认值为**microsoft.windowsupdateplugin**中的插件\-。  
  
### <a name="specify-cau-plug-in-arguments"></a>在参数中指定 CAU 插件\-  
配置更新运行选项时，可以指定一个或多个*名称\=值*对，\) 为中所选的插入\-\(参数。 例如，在 CAU UI 中，你可以指定多个参数，如下所示：  
  
**Name1\=Value1;Name2\=Value2;Name3\=Value3**  
  
对于指定的插件\-，这些*名称\=值*对必须是有意义的。 对于某些插入\-，这些参数是可选的。  
  
自变量中的 CAU 插件\-的语法遵循以下通用规则：  
  
-   多个*名称\=值*对之间用分号分隔。  
  
-   包含空格的值括在引号中，例如： **Name1\="带有空格的值"** 。  
  
-   *值*的确切语法取决于中的插件\-。  
  
若要使用支持 **– CauPluginParameters**参数的 CAU PowerShell cmdlet 指定插件\-参数，请传递以下形式的参数：  
  
**\-CauPluginArguments @ {Name1\=Value1;Name2\=Value2;Name3\=Value3}**  
  
你还可以使用预定义的 PowerShell 哈希表。 若要在中指定多个插件\-的 "插入\-" 参数，请传递多个用逗号分隔的哈希表。 按**CauPluginName**中指定的顺序在插件\-中按参数传递插件\-。  
  
### <a name="specify-optional-plug-in-arguments"></a>在参数中指定可选的插件\-  
CAU 安装 \(**microsoft.windowsupdateplugin**和**microsoft.hotfixplugin**\) 的插件\-提供可选择的其他选项。 在 CAU UI 中，在你为中的\-插件配置更新运行选项之后，这些选项将显示在 "**其他选项**" 页上。 如果你使用的是 CAU PowerShell cmdlet，则在参数中将这些选项配置为可选的插件\-。 有关详细信息，请参阅本主题后面部分中的[使用 Microsoft.WindowsUpdatePlugin](#BKMK_WUP) 和[使用 Microsoft.HotfixPlugin](#BKMK_HFP)。  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>使用 Windows PowerShell cmdlet 管理插件\-  
  
|Cmdlet|说明|  
|----------|---------------|  
|[Register-cauplugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/get-cauplugin)|检索有关在本地计算机上注册的一个或多个软件更新\-插件的信息。|  
|[注册-Register-cauplugin]((https://docs.microsoft.com/powershell/module/clusterawareupdating/register-cauplugin))|在本地计算机上注册 CAU 软件更新插件\-。|  
|[取消注册-Register-cauplugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/unregister-cauplugin)|从 CAU 可以使用的插件\-列表中删除软件更新插件\-。 **注意：** 无法注销随 CAU \(**microsoft.windowsupdateplugin**和**microsoft.hotfixplugin**\) 一起安装的插件\-。|  
  
## <a name="using-the-microsoftwindowsupdateplugin"></a><a name="BKMK_WUP"></a>使用 Microsoft.windowsupdateplugin  

**Microsoft.windowsupdateplugin**的默认 "插入\-" 执行以下操作：
- 与每个故障转移群集节点上的 Windows 更新代理通信，以应用在每个节点上运行的 Microsoft 产品所需的更新。
- 直接从 Windows 更新或 Microsoft 更新或\-本地 Windows Server Update Services \(WSUS\) 服务器安装群集更新。
- 仅安装所选的常规分发版本 \(GDR\) 更新。 默认情况下，中的 "插入\-仅适用于重要的软件更新。 不需要配置。 默认配置在每个节点上下载并安装重要的 GDR 更新。 

> [!NOTE]
> 若要应用默认情况下未选择的重要软件更新 \(例如，驱动程序更新\)，可以在参数中配置可选的 "插件\-"。 有关详细信息，请参阅[配置 Windows 更新代理查询字符串](#BKMK_QUERY)。

### <a name="requirements"></a>要求

- 如果使用的故障转移群集和远程更新协调器计算机 \(\) 必须满足 CAU 的要求以及[cau 的要求和最佳做法](cluster-aware-updating-requirements.md)中列出的远程管理所需的配置。
- 查看[对应用 Microsoft 更新的建议](cluster-aware-updating-requirements.md#BKMK_BP_WUA)，然后对你的故障转移群集节点的 Microsoft 更新配置进行任何必要的更改。
- 为了获得最佳结果，我们建议你 \(BPA\) 运行 CAU 最佳做法分析器，以确保正确配置群集和更新环境，以便通过使用 CAU 来应用更新。 有关详细信息，请参阅[测试 CAU 更新的准备情况](cluster-aware-updating-requirements.md#BKMK_BPA)。

> [!NOTE]
> 排除需要接受 Microsoft 许可条款或需要用户交互的更新，并且必须手动安装更新。

### <a name="additional-options"></a>其他选项

或者，您可以指定以下插件\-in 参数，以增加或限制中的插件\-应用的更新集：
- 若要将中的 "插入\-" 配置为在每个节点上应用建议的更新，请在 CAU UI 中的 "**其他选项**" 页上，选中 "**以我接收重要更新的相同方式向我推荐更新"** 复选框。
<br>或者，将 **"IncludeRecommendedUpdates"\="True"** 插头\-在参数中。
- 若要在中配置插件\-以筛选应用于每个群集节点的 GDR 更新类型，请使用**查询**字符串插件\-in 参数指定 Windows 更新代理查询字符串。 有关详细信息，请参阅[配置 Windows 更新代理查询字符串](#BKMK_QUERY)。

### <a name="configure-the-windows-update-agent-query-string"></a><a name="BKMK_QUERY"></a>配置 Windows 更新代理查询字符串  
可以在**microsoft.windowsupdateplugin**中为默认的 "插入\-" 配置一个 "插入\-in" 参数，该参数由 Windows 更新代理 \(WUA\) 查询字符串组成。 根据特定的选择条件，此指令使用 WUA API 来标识一个或多个组的 Microsoft 更新，以便应用到每个节点。 你可以通过使用逻辑“与”或者逻辑“或”组合多个条件。 在插\-in 参数中指定 WUA 查询字符串，如下所示：  
  
**QueryString\="Criterion1\=Value1 and\/或 Criterion2\=Value2 and\/or ..."**  
  
例如，通过使用默认的 **Microsoft.WindowsUpdatePlugin** 参数，**QueryString** 自动选择重要更新，该默认参数使用 **IsInstalled**、**Type**、**IsHidden** 和 **IsAssigned** 条件构造：  
  
**QueryString\="IsInstalled\=0，并且键入\=" Software "和 IsHidden\=0 和 IsAssigned\=1"**  
  
如果指定**QueryString**参数，则该参数将用于代替为中的插件\-配置的默认**查询字符串**。  
  
#### <a name="example-1"></a>示例 1
  
若要配置用于安装由 ID f6ce46c1 标识的特定更新的**QueryString**参数 *\-971c\-43f9\-a2aa\-783df125f003*：  
  
**QueryString\="UpdateID\=" f6ce46c1\-971c\-43f9\-a2aa\-783df125f003 "和 IsInstalled\=0"**  
  
> [!NOTE]  
> 前面的示例适用于使用群集\-感知更新向导应用更新。 如果你想要通过使用 CAU UI\-更新选项来安装特定更新，或者通过使用**Add\-add-cauclusterrole**或**Set\-add-cauclusterrole**PowerShell cmdlet 来安装特定更新，则必须使用两个\-引号字符对 UpdateID 值进行格式设置：  
>   
> **QueryString\="UpdateID\=" "f6ce46c1\-971c\-43f9\-a2aa\-783df125f003" "和 IsInstalled\=0"**  
  
#### <a name="example-2"></a>示例 2
  
若要配置仅安装驱动程序的 **QueryString** 参数：  
  
**QueryString\="IsInstalled\=0，类型\=" Driver "和 IsHidden\=0"**  
  
若要详细了解\-中默认的插件的查询字符串，请参阅**microsoft.windowsupdateplugin**中的搜索条件 \(例如**IsInstalled**\)，以及查询字符串中可以包含的语法，请参阅[WINDOWS 更新代理（WUA） API 参考](https://go.microsoft.com/fwlink/p/?LinkId=223304)中有关搜索条件的部分。  
  
## <a name="use-the-microsofthotfixplugin"></a><a name="BKMK_HFP"></a>使用 Microsoft.hotfixplugin  
可以使用**microsoft.hotfixplugin**中的插件\-来应用 microsoft 有限分发版本 \(LDR\) 更新 \(也称为 "修补程序"，以前称为 "qfe\)"，您可以单独下载这些内容以解决特定的 Microsoft 软件问题。 此插件会从 SMB 文件共享上的根文件夹安装更新，还可以对其进行自定义以应用非\-Microsoft 驱动程序、固件和 BIOS 更新。

> [!NOTE]
> 在知识库文章中，有时可以从 Microsoft 下载修补程序，但也可以根据需要将其提供给客户\-。

### <a name="requirements"></a>要求

- 如果使用的故障转移群集和远程更新协调器计算机 \(\) 必须满足 CAU 的要求以及[cau 的要求和最佳做法](cluster-aware-updating-requirements.md)中列出的远程管理所需的配置。
- 查看[使用 Microsoft.HotfixPlugin 的建议](cluster-aware-updating-requirements.md#BKMK_BP_HF)。
- 为了获得最佳结果，我们建议你 \(BPA\) 模式下运行 CAU 最佳做法分析器，以确保正确配置群集和更新环境，以便通过使用 CAU 来应用更新。 有关详细信息，请参阅[测试 CAU 更新的准备情况](cluster-aware-updating-requirements.md#BKMK_BPA)。
- 获取发布服务器中的更新，并将其复制或提取到服务器消息块 \(SMB\) 文件共享 \(修补程序根文件夹\) 至少支持 SMB 2.0，并且可由所有群集节点和远程更新协调器计算机访问 \(如果在远程\-更新模式中使用 CAU，则\)。 有关详细信息，请参阅本主题后面部分中的[配置修补程序根文件夹结构](#BKMK_HF_ROOT)。 

    > [!NOTE]
    > 默认情况下，中的此插件\-仅安装具有以下文件扩展名的修补程序： .msu、.msi 和 .msp。

- 将 Defaulthotfixconfig.xml \(文件（在安装了 CAU 工具的计算机上的 **% systemroot%\\System32\\WindowsPowerShell\\v1.0\\模块\\clusterawareupdating.dll**文件夹）复制到在其中安装了修补程序的修补程序根文件夹。\) 例如，将配置文件复制到 *\\\\MyFileServer\\修补程序\\根\\* 。 

    > [!NOTE]
    > 若要安装由 Microsoft 和其他更新提供的大部分修补程序，可以使用默认修补程序配置文件而无需任何修改。 如果你的方案需要它，你可以将配置文件作为一项高级任务进行自定义。 例如，配置文件可以包含自定义规则，以便处理具有特定扩展名的修补程序文件或定义特定退出条件的行为。 有关详细信息，请参阅本主题后面部分中的[自定义修补程序配置文件](#BKMK_CONFIG_FILE)。

### <a name="configuration"></a>配置

配置以下设置。 有关详细信息，请参阅本主题中后面部分的链接。
- 包含要应用的更新以及修补程序配置文件的共享修补程序根文件夹的路径。 可以在 CAU UI 中键入此路径，也可以在参数中将**HotfixRootFolderPath\=\<path >** PowerShell 即插\-。 

   > [!NOTE]
   > 你可以将修补程序根文件夹指定为本地文件夹路径，或指定 *\\\\ServerName\\Share\\RootFolderName*格式的 UNC 路径。 可以使用基于域\-的或独立的 DFS 命名空间路径。 但是，在修补程序配置文件中检查访问权限的功能中的插件\-与 DFS 命名空间路径不兼容，因此，如果您配置一个 DFS 命名空间路径，则必须通过使用 CAU UI 或通过配置**DisableAclChecks\=' True '** 插件\-in 参数来禁用对访问权限的检查。
- 承载修补程序根文件夹的服务器上的设置，用于检查访问该文件夹的适当权限，并确保从 SMB 共享文件夹访问的数据的完整性 \(SMB 签名或 SMB 加密\)。 有关详细信息，请参阅[限制对修补程序根文件夹的访问权限](#BKMK_ACL)。

### <a name="additional-options"></a>其他选项

- （可选）将 "插入\-" 配置为，以便在从修补程序文件共享中访问数据时强制进行 SMB 加密。 在 CAU UI 中的 "**其他选项**" 页上，选择 "**访问修补程序根文件夹时要求 SMB 加密**" 选项，或在参数中配置**RequireSMBEncryption\="True"** PowerShell 插件\-。 
  > [!IMPORTANT]
  > 若要借助 SMB 签名或 SMB 加密启用 SMB 数据的完整性，则必须在 SMB 服务器上执行额外的配置步骤。 有关详细信息，请参阅[限制对修补程序根文件夹的访问权限](#BKMK_ACL)中的第 4 步。 如果你选择强制使用 SMB 加密选项，并且修补程序根文件夹未配置为使用 SMB 加密进行访问，则更新运行将失败。
- 或者，禁用针对修补程序根文件夹的足够权限和修补程序配置文件的默认检查。 在 CAU UI 中，选择 "**禁用对修补程序根文件夹和配置文件的管理员访问权限**"，或配置**DisableAclChecks\="True"** 在参数中插入\-。
- （可选）配置**HotfixInstallerTimeoutMinutes\=<Integer>** 参数，以指定修补程序插件\-等待修补程序安装程序进程返回的时间。 \(默认值为30分钟。\) 例如，若要指定两个小时的超时时间，请将**HotfixInstallerTimeoutMinutes\=120**。
- （可选）配置**HotfixConfigFileName \= <name>** 插\-in 参数以指定位于修补程序根文件夹中的修补程序配置文件的名称。 如果未指定，则使用默认名称 DefaultHotfixConfig.xml。
  
### <a name="configure-a-hotfix-root-folder-structure"></a><a name="BKMK_HF_ROOT"></a>配置修补程序根文件夹结构

要使修补程序插件\-正常运行，修补程序必须以 SMB 文件共享中定义良好\-的结构存储在 SMB 文件 \(共享中\)，并且必须使用 CAU UI 或 CAU PowerShell cmdlet，将修补程序插件\-配置为指向修补程序根文件夹的路径。 此路径作为**HotfixRootFolderPath**参数传递给中的插件\-。 如以下示例所示，根据更新需要，你可以为修补程序根文件夹选择多个结构中的一个。 不符合该结构的文件或文件夹将会忽略。  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>示例 1-用于将修补程序应用到所有群集节点的文件夹结构
  
若要指定修补程序应用于所有群集节点，请将它们复制到名为 CAUHotfix 的文件夹中， **\_全部**位于修补程序根文件夹下。 在此示例中， **HotfixRootFolderPath**插\-in 参数设置为 *\\\\MyFileServer\\修补程序\\根\\* 。 **CAUHotfix\_所有**文件夹都包含三个更新，它们将应用于所有群集节点，并且扩展名为 .msu、.msi 和 .msp。 更新文件名称仅用于说明目的。  
  
> [!NOTE]  
> 在此示例和以下示例中，具有默认名称 DefaultHotfixConfig.xml 的修补程序配置文件在修补程序根文件夹中其所需的位置中显示。  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
```  
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>示例 2-用于将某些更新仅应用于特定节点的文件夹结构
  
若要指定仅适用于特定节点的修补程序，请在具有节点名称的修补程序根文件夹下使用子文件夹。 使用群集节点的 NetBIOS 名称，例如，*ContosoNode1*。 然后，将仅适用于此节点的更新移动到该子文件夹。 在下面的示例中， **HotfixRootFolderPath**插\-in 参数设置为 *\\\\MyFileServer\\修补程序\\根\\* 。 **CAUHotfix\_所有**文件夹中的更新将应用于所有群集节点，而*节点 1\_特定\_更新。 msu*将仅应用于*ContosoNode1*。  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
   ContosoNode1\   
      Node1_Specific_Update.msu   
      ...  
```  
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>示例 3-用于应用 .msu、.msi 和 .msp 文件以外更新的文件夹结构
  
默认情况下，**Microsoft.HotfixPlugin** 仅将应用具有 .msu、.msi 或 .msp 扩展名的更新。 但是，某些更新可能具有不同的扩展名，并且需要不同的安装命令。 例如，你可能需要将具有 .exe 扩展名的固件更新应用于群集中的节点。 你可以使用子文件夹配置修补程序根文件夹，该子文件夹指示应安装的特定、非\-默认更新类型。 你还必须配置相应的文件夹安装规则，该规则用于指定修补程序配置 XML 文件中的 `<FolderRules>` 元素内的安装命令。  
  
在下面的示例中， **HotfixRootFolderPath**插\-in 参数设置为 *\\\\MyFileServer\\修补程序\\根\\* 。 多个更新将应用于所有群集节点，并且通过使用 *FolderRule1* 将固件更新 *SpecialHotfix1.exe* 应用于 *ContosoNode1*。 有关在修补程序配置文件中配置 *FolderRule1* 的详细信息，请参阅本主题后面部分中的[自定义修补程序配置文件](#BKMK_CONFIG_FILE)。  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
  
   ContosoNode1\   
      FolderRule1\  
          SpecialHotfix1.exe  
      ...  
```

### <a name="customize-the-hotfix-configuration-file"></a><a name="BKMK_CONFIG_FILE"></a>自定义修补程序配置文件  
修补程序配置文件控制 **Microsoft.HotfixPlugin** 如何在故障转移群集中安装特定修补程序文件类型。 在 HotfixConfigSchema.xsd 文件内定义的配置文件的 XML 架构，该文件位于安装 CAU 工具的计算机上的以下文件夹中：  
  
**% systemroot%\\System32\\WindowsPowerShell\\v1.0\\模块\\Clusterawareupdating.dll 文件夹**  
  
若要自定义修补程序配置文件，将从该位置的示例配置文件 DefaultHotfixConfig.xml 复制到修补程序根文件夹并为你的方案进行适当的修改。  
  
> [!IMPORTANT]  
> 若要应用由 Microsoft 和其他更新所提供的大部分修补程序，可以使用默认修补程序配置文件而无需任何修改。 自定义修补程序配置文件是仅在高级使用方案中才出现的任务。  
  
默认情况下，修补程序配置 XML 文件定义安装规则和针对以下两个修补程序类别的退出条件：  
  
-   带有扩展名的修补程序文件，\-中的插件默认情况下可以安装 \(.msu、.msi 和 .msp 文件\)。  
  
    它们定义为 `<ExtensionRules>` 元素中的 `<DefaultRules>` 元素。 还有一个用于每个默认支持文件类型的 `<Extension>` 元素。 常规 XML 结构如下所示：  
  
    ```xml  
    <DefaultRules>  
        <ExtensionRules>  
          <Extension name="MSI">  
            <!-- Template and ExitConditions elements for installation of .msi files follow -->  
             ...  
          </Extension>  
          <Extension name="MSU">  
            <!-- Template and ExitConditions elements for installation of .msu files follow -->  
             ...  
          </Extension>  
          <Extension name="MSP">  
            <!-- Template and ExitConditions elements for installation of .msp files follow -->  
             ...  
          </Extension>  
             ...  
       </ExtensionRules>  
    </DefaultRules>  
    ```  
  
    如果你需要将某些更新类型应用到你的环境中的所有群集节点，则可以定义其他 `<Extension>` 元素。  
  
-   修补程序或其他不是 .msi、.msu 或 .msp 文件的更新文件，例如，非\-Microsoft 驱动程序、固件和 BIOS 更新。  
  
    每个非\-默认文件类型配置为 `<FolderRules>` 元素中的 `<Folder>` 元素。 `<Folder>` 元素的名称属性必须与将包含相应类型更新的修补程序根文件夹中文件夹的名称相同。 文件夹可以位于**CAUHotfix\_All**文件夹中，也可以位于节点\-特定文件夹中。 例如，如果在修补程序根文件夹中配置 *FolderRule1*，则在 XML 文件中配置以下元素以定义安装模板和该文件夹中更新的退出条件：  
  
    ```xml  
    <FolderRules>  
          <Folder name="FolderRule1">  
            <!-- Template and ExitConditions elements for installation of updates in FolderRule1 follow -->  
             ...  
          </Folder>  
          ...  
    </FolderRules>  
    ```  
  
下表描述了 `<Template>` 属性和可能的 `<ExitConditions>` 子元素。  
  
|`<Template>` 属性|说明|  
|--------------------------|---------------|  
|`path`|在 `<Extension name>` 属性中所定义文件类型的安装程序的完整路径。<p>若要指定修补程序根文件夹结构中的更新文件的路径，请使用 `$update$`。|  
|`parameters`|在 `path`中指定的程序的必需和可选参数字符串。<p>若要指定一个作为修补程序根文件夹结构中的更新文件路径的参数，请使用 `$update$`。|  
  
|`<ExitConditions>` 子元素|说明|  
|---------------------------------|---------------|  
|`<Success>`|定义一个或多个表明指定更新已成功的退出代码。 这是必需的子元素。|  
|`<Success_RebootRequired>`|或者，定义一个或多个退出代码，以表明指定的更新已成功，并且节点必须重新启动。 <br>**注意：** （可选） `<Folder>` 元素可以包含 `alwaysReboot` 特性。 如果设置此属性，它表明如果按照此规则安装修补程序，则返回在 `<Success>`中定义的退出代码之一，此情况可以解释为 `<Success_RebootRequired>` 退出条件。|  
|`<Fail_RebootRequired>`|或者，定义一个或多个退出代码，以表明指定的更新已失败，并且节点必须重新启动。|  
|`<AlreadyInstalled>`|或者，定义一个或多个退出代码，以表明不应用指定的更新，因为它已经安装。|  
|`<NotApplicable>`|或者，定义一个或多个退出代码，以表明不应用指定的更新，因为它不适用于群集节点。|  
  
> [!IMPORTANT]  
> 任何未在 `<ExitConditions>` 中明确定义的退出代码解释为更新失败，并且不重新启动节点。  
  
### <a name="restrict-access-to-the-hotfix-root-folder"></a><a name="BKMK_ACL"></a>限制对修补程序根文件夹的访问  
你必须执行几个步骤来配置 SMB 文件服务器和文件共享以帮助确保仅在 **Microsoft.HotfixPlugin** 的上下文中对修补程序根文件夹的文件和修补程序配置文件进行访问。 这些步骤启用多个功能，从而帮助防止可能在某种程度上危及故障转移群集的修补程序文件篡改。  
  
常规步骤如下所示：  
  
1.  使用插件\-标识用于更新运行的用户帐户  
  
2.  在 SMB 文件服务器上必要的组中配置此用户帐户  
  
3.  配置权限以访问修补程序根文件夹  
  
4.  配置 SMB 数据完整性的设置  
  
5.  在 SMB 服务器上启用 Windows 防火墙规则  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>步骤 1： 使用修补程序插件标识用于更新运行的用户帐户\-
  
在执行使用**microsoft.hotfixplugin**的更新运行期间，cau 中用于检查安全设置的帐户取决于是否在远程\-更新模式或自检模式\-更新模式中使用 cau，如下所示：  
  
-   **远程\-更新模式**对群集具有管理权限的帐户，用于预览和应用更新。  
  
-   **自行\-更新模式**在 Active Directory 为 CAU 群集角色配置的虚拟计算机对象的名称。 这是为 CAU 群集角色在 Active Directory 中预留的虚拟计算机对象的名称或由 CAU 为群集角色生成的名称。 若要获取由 CAU 生成的名称，请运行**Get\-Add-cauclusterrole** CAU PowerShell cmdlet。 在输出中，**ResourceGroupName** 是生成的虚拟计算机对象帐户的名称。  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>步骤 2： 在 SMB 文件服务器上必要的组中配置此用户帐户
  
> [!IMPORTANT]  
> 你必须在 SMB 服务器上作为本地管理员帐户添加用于更新运行的帐户。 如果因为你组织中的安全策略而不允许这样做，则通过以下过程在 SMB 服务器上使用必要的权限来配置此帐户。  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>在 SMB 服务器上配置用户帐户  
  
1.  将用于“更新运行”的帐户添加到 Distributed COM Users 组和以下任一组：超级用户、服务器操作或打印操作员。  
  
2.  若要启用帐户所需的 WMI 权限，请在 SMB 服务器上启动 WMI 管理控制台。 启动 PowerShell，然后键入以下命令：  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  在控制台树中，\-右键单击 " **WMI 控制" \(本地\)** "，然后单击"**属性**"。  
  
4.  单击“安全”，然后展开“根”。  
  
5.  单击“CIMV2”，然后单击“安全”。  
  
6.  将用于更新运行的帐户添加到“组或用户名”列表。  
  
7.  将“执行方法”和“远程启用”权限授予用于更新运行的帐户。  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>步骤 3。 配置权限以访问修补程序根文件夹
  
默认情况下，当你尝试应用更新时，中的修补程序插件\-将检查 NTFS 文件系统权限的配置以访问修补程序根文件夹。 如果文件夹访问权限配置不正确，则在中使用修补\-程序的更新运行可能会失败。  
  
如果在中使用修补程序\-插件的默认配置，请确保文件夹访问权限满足以下要求。  
  
-   用户组具有读取权限。  
  
-   如果中的 "插入\-将使用 .exe 扩展名应用更新，则用户组具有 Execute 权限。  
  
-   只允许某些安全主体 \(但不需要\) 具有写入或修改权限。 允许的主体是本地管理员组、SYSTEM、CREATOR OWNER 和 TrustedInstaller。 其他帐户或组不允许具有写入或修改修补程序根文件夹的权限。  
  
（可选）可以禁用中的 "插入\-默认执行的前面的检查。 可以通过两种方式之一完成此操作：  
  
-   如果使用 CAU PowerShell cmdlet，请在**CauPluginArguments**参数中为修补程序插件\-配置**DisableAclChecks\=' True '** 参数。  
  
-   如果使用 CAU UI，请选择用于配置更新运行选项的向导中“其他更新选项”页面上的“禁用对修补程序根文件夹和配置文件管理员访问权限的检查”选项。  
  
但是，作为在许多环境中的最佳实践，我们建议你使用默认的配置强制执行这些检查。  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>步骤 4. 配置 SMB 数据完整性的设置
  
若要检查群集节点和 SMB 文件共享之间的连接中的数据完整性，修补程序插件\-需要在 SMB 文件共享上启用 SMB 签名或 SMB 加密的设置。 SMB 加密在许多环境中提供了增强的安全性和更好的性能，从 Windows Server 2012 开始受支持。 你可以启用其中一种设置或同时启用这两种设置，如下所示：  
  
-   若要启用 SMB 签名，请参阅 Microsoft 知识库内的 [文章 887429](https://support.microsoft.com/kb/887429) 中描述的过程。  
  
-   若要为 SMB 共享文件夹启用 SMB 加密，请在 SMB 服务器上运行以下 PowerShell cmdlet：  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    其中 <*ShareName*> 是 SMB 共享文件夹的名称。  
  
（可选）若要在 SMB 服务器的连接中强制使用 SMB 加密，请选择 CAU UI 中的 "**访问修补程序根文件夹时要求使用 Smb 加密**" 选项，或使用 cau PowerShell Cmdlet 配置**RequireSMBEncryption\=' True '** 插件\-in 参数。  
  
> [!IMPORTANT]  
> 如果你选择强制使用 SMB 加密的选项，并且修补程序根文件夹未配置为使用 SMB 加密的连接，则更新运行将失败。  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>步骤 5： 在 SMB 服务器上启用 Windows 防火墙规则
  
你必须在 SMB 文件服务器上的 Windows 防火墙中\)规则中启用**文件服务器远程管理 \(smb\-** 。 默认情况下，在 Windows Server 2016、Windows Server 2012 R2 和 Windows Server 2012 中启用此功能。  
  
## <a name="see-also"></a>另请参阅  
  
-   [群集感知更新概述](cluster-aware-updating.md)
  
-   [群集感知更新 Windows PowerShell Cmdlet](https://docs.microsoft.com/powershell/module/clusterawareupdating)  
  
-   [群集感知更新插件参考](https://msdn.microsoft.com/library/hh418084.aspx)  
  
