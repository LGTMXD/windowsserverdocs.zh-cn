---
title: 部署漫游用户策略文件
TOCTitle: Deploying Roaming User Profiles
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.date: 06/07/2019
ms.author: jgerend
ms.openlocfilehash: 8feed2adb606edfb6068d7fe10c18baf142077ac
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "76822340"
---
# <a name="deploying-roaming-user-profiles"></a>部署漫游用户策略文件

>适用于：Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2019、Windows Server 2016、Windows Server（半年频道）、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

本主题介绍了如何使用 Windows Server 将[漫游用户策略文件](folder-redirection-rup-overview.md)部署到 Windows 客户端计算机。 漫游用户策略文件将用户配置文件重定向到文件共享，以便用户可在多台计算机上检索相同的操作系统和应用程序设置。

有关本主题最近更改的列表，请参阅本主题的[更改历史记录](#change-history)部分。

> [!IMPORTANT]
> 由于 [MS16-072 ](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016) 中所做的安全更改，我们更新了本主题中的[步骤 4：（可选）为漫游用户策略文件创建 GPO](#step-4-optionally-create-a-gpo-for-roaming-user-profiles)，以便 Windows 可以正确应用漫游用户策略文件策略（而不是还原到受影响的电脑上的本地策略）。

> [!IMPORTANT]
>  在以下配置中，操作系统就地升级后，用户对“开始”的自定义设置将丢失：
> - 系统将针对漫游配置文件配置用户
> - 系统允许用户对“开始”进行更改
>
> 因此，在操作系统就地升级之后，“开始”菜单将重置为新操作系统版本的默认设置。 有关解决方法，请参阅[附录 C：解决升级后重置“开始”菜单布局的问题](#appendix-c-working-around-reset-start-menu-layouts-after-upgrades)。

## <a name="prerequisites"></a>必备条件

### <a name="hardware-requirements"></a>硬件要求

漫游用户策略文件需要基于 x64 的计算机或基于 x86 的计算机；它不受 Windows RT 支持。

### <a name="software-requirements"></a>软件要求

漫游用户配置文件有以下软件要求：

- 如果要在具有现有本地用户配置文件的环境中部署带有文件夹重定向的漫游用户配置文件，则在部署漫游用户配置文件之前先部署文件夹重定向，以最大程度减小漫游配置文件。 在成功重定向现有的用户文件夹后，可部署漫游用户配置文件。
- 若要管理漫游用户配置文件，你必须以域管理员安全组、企业管理员安全组或组策略创建者所有者安全组成员身份登录。
- 客户端计算机必须运行 Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 或 Windows Server 2008。
- 客户端计算机必须加入你管理的 Active Directory 域服务 (AD DS)。
- 必须提供一台安装了组策略管理和 Active Directory 管理中心的计算机。
- 必须提供文件服务器，才能托管漫游用户配置文件。

    - 如果文件共享使用 DFS 命名空间，则 DFS 文件夹（链接）必须具有单个目标，以防止用户在不同服务器上进行互相冲突的编辑。
    - 如果文件共享使用 DFS 复制与另一台服务器复制内容，则用户必须只能够访问源服务器，以防止用户在不同服务器上进行互相冲突的编辑。
    - 如果文件共享已群集化，则在文件共享上禁用连续可用性，以免出现性能问题。
- 若要使用漫游用户策略文件中的主计算机支持，还需满足其他客户端计算机和 Active Directory 架构要求。 有关详细信息，请参阅[为文件夹重定向以及漫游用户策略文件部署主计算机](deploy-primary-computers.md)。
- 如果用户使用多台电脑、远程桌面会话主机或虚拟桌面基础结构 (VDI) 服务器，则用户的“开始”菜单的布局不会在 Windows 10、Windows Server 2019 或 Windows Server 2016 上漫游。 作为一种解决方法，可以如本主题中所述指定“开始”布局。 或者还可以使用用户配置文件磁盘，它在与远程桌面会话主机服务器或 VDI 服务器一起使用时可正确地漫游“开始”菜单设置。 有关详细信息，请参阅[使用 Windows Server 2012 中的用户配置文件磁盘实现更轻松的用户数据管理](https://blogs.technet.microsoft.com/enterprisemobility/2012/11/13/easier-user-data-management-with-user-profile-disks-in-windows-server-2012/)。

### <a name="considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows"></a>在多个版本的 Windows 中使用漫游用户配置文件时的注意事项

如果你决定跨多个版本的 Windows 使用漫游用户配置文件，我们建议采取下列措施：

- 配置 Windows 来为每个操作系统版本维护单独的配置文件版本。 这有助于防止不必要和不可预知的问题（如配置文件损坏）。
- 使用文件夹重定向来将用户文件（如文档和图片）存储在用户配置文件之外。 这使用户可以跨不同操作系统版本使用相同文件。 它还能保持配置文件具有较小的大小并保持快速登录。
- 为漫游用户配置文件分配足够的存储空间。 如果支持两个操作系统版本，则配置文件的数目将增加一倍（因此占用了总空间），因为将为每个操作系统版本维护单独的配置文件。
- 不要在运行 Windows Vista/Windows Server 2008 和 Windows 7/Windows Server 2008 R2 的计算机之间使用漫游用户策略文件。 由于这些操作系统的配置文件版本不兼容，所以不支持在这些版本之间漫游。
- 请告知用户，在一个操作系统版本上进行的更改将不会漫游到另一个操作系统版本。
- 将环境移动到使用不同配置文件版本的 Windows 版本时（例如，从 Windows 10 移动到 Windows 10 版本 1607 - 参阅[附录 B：配置文件版本参考信息](#appendix-b-profile-version-reference-information)获取列表），用户将收到一个新的空漫游用户策略文件。 通过使用文件夹重定向来重定向常用文件夹，可最大限度地减少获取新配置文件所造成的影响。 不支持任何将漫游用户策略文件从一个配置文件版本迁移到另一个版本的方法。

## <a name="step-1-enable-the-use-of-separate-profile-versions"></a>步骤 1：支持使用单独的配置文件版本

如果要在运行 Windows 8.1、Windows 8、Windows Server 2012 R2 或 Windows Server 2012 的计算机上部署漫游用户策略文件，建议在部署之前先对 Windows 环境进行一些更改。 这些更改有助于确保将来的操作系统升级顺利进行，并且有助于同时运行多个版本带有漫游用户配置文件的 Windows。

若要进行这些更改，请使用以下过程。

1. 在要使用漫游、强制、超级强制或域默认配置文件的所有计算机上，下载并安装相应的软件更新：

    - Windows 8.1 或 Windows Server 2012 R2：安装 Microsoft 知识库的文章 [2887595](https://support.microsoft.com/kb/2887595) 中所述的软件更新（如已发布）。
    - Windows 8 或 Windows Server 2012：安装 Microsoft 知识库的文章 [2887239](https://support.microsoft.com/kb/2887239) 中所述的软件更新。

2. 在将使用漫游用户策略文件的运行 Windows 8.1、Windows 8、Windows Server 2012 R2 或 Windows Server 2012 的所有计算机上，使用注册表编辑器或组策略来创建以下注册表项 DWORD 值，并将其设置为“`1`”。 有关使用组策略创建注册表项的信息，请参阅 [配置注册表项](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>)。

    ```
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ProfSvc\Parameters\UseProfilePathExtensionVersion
    ```

    > [!WARNING]
    > 不正确地编辑注册表可能会对系统造成严重损坏。 在更改注册表之前，应备份计算机上任何有价值的数据。
3. 重新启动计算机。

## <a name="step-2-create-a-roaming-user-profiles-security-group"></a>步骤 2：创建漫游用户配置文件安全组

如果你的环境尚未设置漫游用户配置文件，则第一步是创建一个安全组，其中包含你希望应用漫游用户配置文件策略设置的所有用户和/或计算机。

- 通用漫游用户配置文件部署的管理员通常创建用户的安全组。
- 远程桌面服务或虚拟化桌面部署的管理员通常使用用户和共享计算机的安全组。

下面介绍如何创建用于漫游用户策略文件的安全组：

1. 在装有 Active Directory 管理中心的计算机上打开服务器管理器。
2. 在“工具”菜单上，选择“Active Directory 管理中心”   。 此时将出现 Active Directory 管理中心。
3. 右键单击相应的域或 OU，选择“新建”，然后选择“组”   。
4. 在“创建组”  窗口的“组”  部分，指定以下设置：

    - 在“组名”  中，键入安全组的名称，例如：**漫游用户配置文件相关用户和计算机**。
    - 在“组范围”中，选择“安全性”，然后选择“全局”    。

5. 在“成员”部分中选择“添加”   。 此时将出现“选择用户、联系人、计算机、服务帐户或组”对话框。
6. 如果要将计算机帐户包括在安全组中，请依次选择“对象类型”、“计算机”复选框，然后选择“确定”    。
7. 请键入希望向其部署漫游用户策略文件的用户、组和/或计算机的名称，选择“确定”，然后再次选择“确定”   。

## <a name="step-3-create-a-file-share-for-roaming-user-profiles"></a>步骤 3:创建用于漫游用户配置文件的文件共享

如果还没有单独用于漫游用户策略文件的文件共享（独立于任何用于重定向文件夹的共享，以防止意外缓存漫游配置文件文件夹），请使用以下过程在运行 Windows Server 的服务器上创建文件共享。

> [!NOTE]
> 某些功能可能会有所不同或不可用，具体取决于所使用的 Windows Server 版本。

下面介绍如何在 Windows Server 上创建文件共享：

1. 在“服务器管理器”导航窗格中，选择“文件和存储服务”，然后选择“共享”以显示“共享”页   。
2. 在“共享”磁贴中，选择“任务”，然后选择“新建共享”   。 此时将出现新建共享向导。
3. 在“选择配置文件”页上，选择“SMB 共享 - 快速”   。 如果已安装文件服务器资源管理器并且要使用文件夹管理属性，则改为选择“SMB 共享 - 高级”  。
4. 在“共享位置”  页上，选择你要在其上创建共享的服务器和卷。
5. 在“共享名”  页上，在“共享名”  框中键入共享的名称（例如， **用户配置文件$** ）。

    > [!TIP]
    > 在创建共享时，通过在共享名后放置 ```$``` 来隐藏共享。 这会在普通浏览器中隐藏共享。

6. 在“其他设置”  页上，清除“启用连续可用性”  复选框（如果存在），并且可以选择性地选中“启用基于访问的枚举”  和“加密数据访问”  复选框。
7. 在“权限”页面，选择“自定义权限…”   。 将出现高级安全设置对话框。
8. 选择“禁用继承”，然后选择“将此对象上的继承权限转换为显式权限”   。
9. 请按照[漫游用户策略文件的文件共享的所需权限](#required-permissions-for-the-file-share-hosting-roaming-user-profiles)中所述和以下屏幕截图中所示来设置权限，删除未列出的组和帐户的权限，并将特殊权限添加到在步骤 1 中创建的漫游用户策略文件用户和计算机组。
    
    ![显示表 1 所述权限的“高级安全设置”窗口](media/advanced-security-user-profiles.jpg)
    
    **图 1** 设置漫游用户配置文件共享的权限
10. 如果选择了“SMB 共享 – 高级”  配置文件，则在“管理属性”  页上，选择“用户文件”  文件夹使用值。
11. 如果选择了“SMB 共享 – 高级”  配置文件，则在“配额”  页上选择性地选择要应用于共享用户的配额。
12. 在“确认”页面，选择“创建”   。

### <a name="required-permissions-for-the-file-share-hosting-roaming-user-profiles"></a>托管漫游用户策略文件的文件共享的所需权限

| 用户帐户 | 访问 | 适用于 |
|   -   |   -   |   -   |
|   System    |  完全控制     |  此文件夹、子文件夹和文件     |
|  Administrators     |  完全控制     |  仅此文件夹     |
|  创建者/所有者     |  完全控制     |  仅子文件夹和文件     |
| 需要将数据放在共享中的用户（漫游用户配置文件用户和计算机）的安全组      |  列出文件夹/读取数据（高级权限）  <br />创建文件夹/附加数据（高级权限）  |  仅此文件夹     |
| 其他组和帐户   |  无（删除）     |       |

## <a name="step-4-optionally-create-a-gpo-for-roaming-user-profiles"></a>步骤 4：（可选）为漫游用户配置文件创建 GPO

如果尚未为漫游用户配置文件设置创建 GPO，请使用以下过程创建一个空白 GPO 以用于漫游用户配置文件。 此 GPO 允许你配置漫游用户配置文件设置（如主计算机支持，将对此进行单独讨论），并且还可用于在计算机上启用漫游用户配置文件，这与在虚拟化桌面环境中部署时或使用远程桌面服务部署时通常采用的做法一样。

下面介绍了如何为漫游用户策略文件创建 GPO：

1. 在装有组策略管理的计算机上打开服务器管理器。
2. 从“工具”菜单上选择“组策略管理”   。 将出现“组策略管理”
3. 右键单击要在其中安装漫游用户策略文件的域或 OU，然后选择“在此域中创建 GPO 并将其链接在此处”  。
4. 在“新键 GPO”对话框中，键入 GPO 的名称（例如漫游用户策略文件设置），然后选择“确定”    。
5. 右键单击新创建的 GPO，然后清除“已启用链接”  复选框。 这将阻止应用该 GPO，直到已完成对它的配置为止。
6. 选中该 GPO。 在“范围”选项卡的“安全筛选”部分，选择“经过身份验证的用户”，然后选择“删除”以防止 GPO 应用于所有人     。
7. 在“安全筛选”部分中，选择“添加”   。
8. 在“选择用户、计算机或组”对话框中，键入在步骤 1 中创建的安全组名称（例如“漫游用户策略文件用户和计算机”），然后选择“确定”    。
9. 依次选择“委派”选项卡、“添加”，键入“经过身份验证的用户”，选择“确定”，然后再次选择“确定”以接受默认读取权限      。
    
    由于 [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016) 中所做的安全更改，因此此步骤是必需的。

>[!IMPORTANT]
>由于 [MS16-072A](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016) 中所做的安全更改，现在必须向“经过身份验证的用户组”委派对 GPO 的读取权限 - 否则，GPO 将不会应用于用户；或者，如果已应用 GPO，则会删除 GPO，并将用户配置文件重定向回本地电脑。 有关详细信息，请参阅[部署组策略安全更新 MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/)。

## <a name="step-5-optionally-set-up-roaming-user-profiles-on-user-accounts"></a>步骤 5：（可选）在用户帐户上设置漫游用户配置文件

如果你要将漫游用户配置文件部署到用户帐户，请使用以下过程在 Active Directory 域服务中指定用于用户帐户的漫游用户配置文件。 如果要将漫游用户策略文件部署到计算机（像通常对远程桌面服务或虚拟化桌面部署采用的做法一样），则改用[步骤 6：（可选）在计算机上设置漫游用户策略文件](#step-6-optionally-set-up-roaming-user-profiles-on-computers)中记录的过程。

> [!NOTE]
> 如果你使用 Active Directory 在用户帐户上设置漫游用户配置文件，并使用组策略在计算机上进行设置，则基于计算机的策略设置优先级较高。

下面介绍了如何在用户帐户上设置漫游用户策略文件：

1. 在 Active Directory 管理中心中，导航到相应域中的“用户”  容器（或 OU）。
2. 选择希望向其分配漫游用户策略文件的所有用户，右键单击这些用户，然后选择“属性”  。
3. 在“配置文件”部分，选中“配置文件路径:”复选框，然后输入要存储用户漫游用户策略文件的文件共享所在的路径，后跟 `%username%`（在用户第一次登录时，这将自动替换为用户名）   。 例如：
    
    `\\fs1.corp.contoso.com\User Profiles$\%username%`
    
    若要指定强制漫游用户策略文件，请指定指向之前创建的 NTuser.man 文件的路径，例如 `fs1.corp.contoso.comUser Profiles$default`。 有关详细信息，请参阅[创建强制用户配置文件](https://docs.microsoft.com/windows/client-management/mandatory-user-profile)。
4. 选择“确定”  。

> [!NOTE]
> 默认情况下，在使用漫游用户配置文件时，允许部署所有基于 Windows ® 运行时的（Windows 应用商店）应用。 但是，在使用特殊配置文件时，默认情况下将不部署应用。 特殊配置文件是在用户注销后放弃所做更改的用户配置文件：
> <br><br>若要删除对特殊配置文件的应用部署的限制，请启用 **Allow deployment operations in special profiles** 策略设置（位于计算机配置\策略\管理模板\Windows 组件\应用程序包部署中）。 但在此情况下，已部署的应用将在计算机上存储一些数据，这些数据可能会累积，例如一台计算机有数百位用户的情况。 若要清理应用，请查找或开发一种使用 [CleanupPackageForUserAsync](https://msdn.microsoft.com/library/windows/apps/windows.management.deployment.packagemanager.cleanuppackageforuserasync.aspx) API 的工具，来清理在计算机上不再有配置文件的用户的应用包。
> <br><br>有关 Windows 应用商店应用的其他背景信息，请参阅 [管理客户端对 Windows 应用商店的访问](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh832040(v=ws.11)>)。

## <a name="step-6-optionally-set-up-roaming-user-profiles-on-computers"></a>步骤 6：（可选）在计算机上设置漫游用户配置文件

如果你要将漫游用户配置文件部署到计算机（像通常对远程桌面服务或虚拟化桌面部署的做法一样），请使用以下过程。 如果要将漫游用户策略文件部署到用户帐户，则改为使用[步骤 5：（可选）在用户帐户上设置漫游用户策略文件](#step-5-optionally-set-up-roaming-user-profiles-on-user-accounts)中所述的过程。

可以使用组策略将漫游用户策略文件应用于运行 Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2，或 Windows Server 2008 的计算机。

> [!NOTE]
> 如果你使用组策略在计算机上设置漫游用户配置文件，并使用 Active Directory 在用户帐户上进行设置，则基于计算机的策略设置具有较高优先级。

下面介绍了如何在计算机上设置漫游用户策略文件：

1. 在装有组策略管理的计算机上打开服务器管理器。
2. 从“工具”菜单上，选择“组策略管理”   。 “组策略管理”将随即出现。
3. 在“组策略管理”中，右键单击在第 3 步中创建的 GPO（例如“漫游用户策略文件设置”），然后选择“编辑”   。
4. 在组策略管理编辑器窗口中，依次导航到“计算机配置”  、“策略”  、“管理模板”  、“系统”  、“用户配置文件”  。
5. 右键单击“为登录此计算机的所有用户设置漫游配置文件路径”，然后选择“编辑”   。
    > [!TIP]
    > 用户的主文件夹（如果已配置）是某些程序（如 Windows PowerShell）使用的默认文件夹。 你可以使用 AD DS 中用户帐户属性的“主文件夹”  部分，为每个用户配置备用的本地或网络位置。 若要在虚拟桌面环境中为运行 Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2 或 Windows Server 2012 的计算机的所有用户配置主文件夹位置，请启用“设置用户主文件夹”策略设置，然后指定要映射的文件共享和驱动器号（或指定一个本地文件夹）  。 请不要使用环境变量或省略号。 用户的别名将附加到用户登录期间指定的路径末尾。
6. 在“属性”对话框中，选择“已启用”  
7. 在“登录此计算机的用户应使用此漫游配置文件路径”框中，输入要存储用户漫游用户策略文件的文件共享所在的路径，后跟 `%username%`（这将在用户第一次登录时自动替换为用户名）  。 例如：

    `\\fs1.corp.contoso.com\User Profiles$\%username%`

    若要指定强制漫游用户策略文件（这是用户无法进行永久性更改的预配置配置文件，将在用户注销后重置已进行的更改），请指定指向之前创建的 NTuser.man 文件的路径，例如 `\\fs1.corp.contoso.com\User Profiles$\default`。 有关详细信息，请参阅 [创建强制用户配置文件](https://docs.microsoft.com/windows/client-management/mandatory-user-profile)。
8. 选择“确定”  。

## <a name="step-7-optionally-specify-a-start-layout-for-windows-10-pcs"></a>步骤 7：（可选）为 Windows 10 电脑指定“开始”布局

可使用组策略来应用特定的“开始”菜单布局，以便用户在所有电脑上看到相同的“开始”布局。 如果用户登录到多台电脑，并且你希望他们在多台电脑上有一致的“开始”布局，请确保 GPO 应用于其所有电脑。

若要指定“开始”布局，请执行以下操作：

1. 将 Windows 10 电脑更新到 Windows 10 版本 1607（也称为周年更新）或更新版本，并安装 2017 年 3 月 14 日累积更新 ([KB4013429](https://support.microsoft.com/kb/4013429)) 或更新版本。
2. 创建完全或部分“开始”菜单布局 XML 文件。 为此，请参阅[自定义和导出“开始”布局](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)。
    * 如果指定完全“开始”布局，用户将无法自定义“开始”菜单的任何部分  。 如果指定部分“开始”布局，用户可以自定义除指定的磁贴组以外的所有内容  。 但是，对于部分“开始”布局，用户对“开始”菜单的自定义设置将不会漫游到其他电脑。
3. 使用组策略将自定义的“开始”布局应用于为漫游用户策略文件创建的 GPO。 为此，请参阅[使用组策略以在域中应用自定义的“开始”布局](https://docs.microsoft.com/windows/configuration/customize-windows-10-start-screens-by-using-group-policy#bkmk-domaingpodeployment)。
4. 使用组策略在 Windows 10 电脑上设置以下注册表值。 为此，请参阅[配置注册表项](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>)。

| **操作**   | **Update**                  |
| ------------ | ------------                |
| 配置单元         | HKEY_LOCAL_MACHINE       |
| 注册表项路径     | Software\Microsoft\Windows\CurrentVersion\Explorer  |
| 值名称   | SpecialRoamingOverrideAllowed  |
| 值类型   | REG_DWORD                |
| “数值数据”   | 1（或 0 以禁用）   |
| 基本         | 十进制                  |

5. （可选）启用首次登录优化，使用户能够更快登录。 为此，请参阅[应用策略以改进登录时间](https://docs.microsoft.com/windows/client-management/mandatory-user-profile#apply-policies-to-improve-sign-in-time)。
6. （可选）通过从用于部署客户端电脑的 Windows 10 基本映像删除不必要的应用，进一步缩短登录时间。 Windows Server 2019 和 Windows Server 2016 没有任何预配的应用，因此可以跳过服务器映像的此步骤。
    - 若要删除应用，请使用 [Windows PowerShell 中的 Remove-AppxProvisionedPackage ](https://docs.microsoft.com/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps)cmdlet 来卸载以下应用程序。 如果电脑已部署，则可以使用 [Remove-AppxPackage ](https://docs.microsoft.com/powershell/module/appx/remove-appxpackage?view=win10-ps) 为删除这些应用编写脚本。
    
      - Microsoft.windowscommunicationsapps\_8wekyb3d8bbwe
      - Microsoft.BingWeather\_8wekyb3d8bbwe
      - Microsoft.DesktopAppInstaller\_8wekyb3d8bbwe
      - Microsoft.Getstarted\_8wekyb3d8bbwe
      - Microsoft.Windows.Photos\_8wekyb3d8bbwe
      - Microsoft.WindowsCamera\_8wekyb3d8bbwe
      - Microsoft.WindowsFeedbackHub\_8wekyb3d8bbwe
      - Microsoft.WindowsStore\_8wekyb3d8bbwe
      - Microsoft.XboxApp\_8wekyb3d8bbwe
      - Microsoft.XboxIdentityProvider\_8wekyb3d8bbwe
      - Microsoft.ZuneMusic\_8wekyb3d8bbwe

>[!NOTE]
>卸载这些应用会缩短登录时间，但如果部署需要，可以将其保留为安装状态。

## <a name="step-8-enable-the-roaming-user-profiles-gpo"></a>步骤 8：启用漫游用户配置文件 GPO

如果你使用组策略在计算机上设置漫游用户配置文件，或者如果使用组策略自定义其他漫游用户配置文件设置，则下一步是启用 GPO，以允许将其应用于受影响的用户。

>[!TIP]
>如果计划实现主计算机支持，现在请进行该操作，然后再启用 GPO。 这会防止在启用主计算机支持之前将用户数据复制到非主计算机。 有关特定策略设置的详细信息，请参阅[为文件夹重定向以及漫游用户策略文件部署主计算机](deploy-primary-computers.md)。

下面介绍了如何启用漫游用户策略文件 GPO：

1. 打开“组策略管理”。
2. 右键单击创建的 GPO，然后选择“已启用链接”  。 菜单项旁边会出现一个复选框。

## <a name="step-9-test-roaming-user-profiles"></a>步骤 9：测试漫游用户配置文件

若要测试漫游用户配置文件，请登录到一台已针对漫游用户配置文件配置用户帐户的计算机，或登录到已针对漫游用户配置文件进行配置的计算机。 然后确认已将该配置文件重定向。

下面介绍了如何测试漫游用户策略文件：

1. 登录到主计算机（如果已启用主计算机支持），该计算机具有你已启用漫游用户配置文件的用户帐户。 如果你已在特定计算机上启用漫游用户配置文件，则登录到其中一台计算机。
2. 如果用户以前已登录到计算机，则打开提升的命令提示符，然后键入以下命令以确保最新的组策略设置已应用到客户端计算机：
    
    ```PowerShell
    GpUpdate /Force
    ```
3. 若要确认该用户配置文件正在漫游，请打开“控制面板”，依次选择“系统和安全”、“系统”、“高级系统设置”、“用户配置文件”部分中的“设置”，然后在“类型”列中查找“漫游”        。

## <a name="appendix-a-checklist-for-deploying-roaming-user-profiles"></a>附录 A：有关部署漫游用户配置文件的清单

| 状态                     | 操作                                                |
| ---                        | ------                                                |
| ☐<br>☐<br>☐<br>☐<br>☐   | 1.准备域<br>- 将计算机加入到域<br>- 支持使用单独的配置文件版本<br>- 创建用户帐户<br>-（可选）部署文件夹重定向 |
| ☐<br><br><br>             | 2.创建漫游用户配置文件的安全组<br>- 组名：<br>- 成员： |
| ☐<br><br>                 | 3.创建用于漫游用户配置文件的文件共享<br>- 文件共享名： |
| ☐<br><br>                 | 4.创建用于漫游用户配置文件的 GPO<br>- GPO 名称：|
| ☐                         | 5.配置漫游用户配置文件策略设置    |
| ☐<br>☐<br>☐              | 6.启用漫游用户策略文件<br>- 在用户帐户上的 AD DS 中启用？<br>- 在计算机帐户上的组策略中启用？<br> |
| ☐                         | 7.（可选）为 Windows 10 电脑指定强制的“开始”布局 |
| ☐<br>☐<br><br>☐<br><br>☐ | 8.（可选）启用主计算机支持<br>- 为用户指定主计算机<br>- 用户和主计算机映射的位置：<br>-（可选）为文件夹重定向启用主计算机支持<br>- 基于计算机还是基于用户？<br>-（可选）为漫游用户策略文件启用主计算机支持 |
| ☐                        | 9.启用漫游用户配置文件 GPO                |
| ☐                        | 10.测试漫游用户配置文件                         |

## <a name="appendix-b-profile-version-reference-information"></a>附录 B：配置文件版本参考信息

每个配置文件都有一个配置文件版本，该版本大致对应于使用该配置文件的 Windows 版本。 例如，Windows 10 版本 1703 和版本 1607 均使用 .V6 配置文件版本。 Microsoft 仅在必要时才创建新的配置文件版本来维持兼容性，这就是每个 Windows 版本都不包含新配置文件版本的原因。

下表列出了各种版本的 Windows 上漫游用户配置文件的位置。

| 操作系统版本 | 漫游用户配置文件位置 |
| --- | --- |
| Windows XP 和 Windows Server 2003 | ```\\<servername>\<fileshare>\<username>``` |
| Windows Vista 和 Windows Server 2008 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 7 和 Windows Server 2008 R2 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 8 和 Windows Server 2012 | ```\\<servername>\<fileshare>\<username>.V3```（在应用软件更新和注册表项后）<br>```\\<servername>\<fileshare>\<username>.V2```（在应用软件更新和注册表项前） |
| Windows 8.1 和 Windows Server 2012 R2 | ```\\<servername>\<fileshare>\<username>.V4```（在应用软件更新和注册表项后）<br>```\\<servername>\<fileshare>\<username>.V2```（在应用软件更新和注册表项前） |
| Windows 10 | ```\\<servername>\<fileshare>\<username>.V5``` |
| Windows 10 版本 1703 及版本 1607 | ```\\<servername>\<fileshare>\<username>.V6``` |

## <a name="appendix-c-working-around-reset-start-menu-layouts-after-upgrades"></a>附录 C：解决升级后重置“开始”菜单布局的问题

下面是一些解决就地升级之后“开始”菜单布局重置的方法：

- 如果只有一个用户使用该设备，并且 IT 管理员使用诸如“配置服务器”的托管操作系统部署策略，则可以执行以下操作：
    
  1. 升级前，使用 Export-Startlayout 导出“开始”菜单布局 
  2. 在 OOBE 之后但在用户登录之前，使用 Import-StartLayout 导入“开始”菜单布局  
 
     > [!NOTE] 
     > 导入 StartLayout 会修改默认用户配置文件。 导入后创建的所有用户配置文件都将获得导入的开始布局。
 
- IT 管理员可以选择通过组策略管理“开始”的布局。 使用组策略可提供集中式的管理解决方案，用于向用户应用标准化的“开始”布局。 有两种模式可使用组策略进行“开始”管理。 完全锁定和部分锁定。 完全锁定方案可阻止用户对“开始”布局进行任何更改。 部分锁定方案可允许用户对特定的“开始”区域进行更改。 有关详细信息，请参阅[自定义和导出“开始”布局](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)。
        
   > [!NOTE]
   > 在部分锁定方案中进行的用户更改在升级过程中仍将丢失。

- 允许“开始”布局重置，并允许最终用户重新配置“开始”。 可以向最终用户发送通知电子邮件或其他通知，告知“开始”布局将在操作系统升级后重置，以便将影响降到最低。 

## <a name="change-history"></a>更改历史记录

下表总结了一些对本主题进行的最重要的更改。

| 日期 | 说明 |原因|
| --- | ---         | ---   |
| 2019 年 5 月 1 日 | 增加对 Windows Server 2019 的更新 |
| 2018 年 4 月 10 日 | 增加有关操作系统就地升级后用户对“开始”的自定义设置丢失的讨论|标注已知问题。 |
| 2018 年 3 月 13 日 | 针对 Windows Server 2016 进行更新 | 从以前版本的库中移出，并针对当前版本的 Windows Server 进行更新。 |
| 2017 年 4 月 13 日 | 增加 Windows 10 版本 1703 的配置文件信息，并阐明如何在升级操作系统时漫游配置文件版本，请参阅[在多个版本的 Windows 上使用漫游用户策略文件时的注意事项](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows)。 | 客户反馈。 |
| 2017 年 3 月 14 日 | 在[附录 A：有关部署漫游用户策略文件的清单](#appendix-a-checklist-for-deploying-roaming-user-profiles)中增加了为 Windows 10 电脑指定强制“开始”布局的可选步骤。 |最新的 Windows 更新中的功能更改。 |
| 2017 年 1 月 23 日 | 向[步骤 4：（可选）为漫游用户策略文件创建 GPO](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) 中添加了一个步骤，以将读取权限委派给经过身份验证的用户，由于组策略安全更新，这现在是必需的权限。|组策略处理的安全更改。 |
| 2016 年 12 月 29 日 | 在[步骤 8：启用漫游用户策略文件 GPO](#step-8-enable-the-roaming-user-profiles-gpo) 中添加了一个链接，以便更容易地获取有关如何为主计算机设置组策略的信息。 此外，还修复了几个对步骤 5 和步骤 6 的引用，这些引用中存在数字错误。|客户反馈。 |
| 2016 年 12 月 5 日 | 增加了解释“开始”菜单设置漫游问题的信息。 | 客户反馈。 |
| 2016 年 7 月 6 日 | 在[附录 B：配置文件版本参考信息](#appendix-b-profile-version-reference-information)中添加了 Windows 10 配置文件版本后缀。 还从支持的操作系统的列表中删除了 Windows XP 和 Windows Server 2003。 | 针对新版本 Windows 的更新，并删除了有关不再受支持的 Windows 版本的信息。 |
| 2015 年 7 月 7日 | 添加了在使用群集文件服务器时禁用连续可用性的要求和步骤。 | 禁用连续可用性后，群集文件共享可以为小型写入操作（对于漫游用户配置文件很常见）提供更好的性能。 |
| 2014 年 3 月 19 日 | 将[附录 B：配置文件版本参考信息](#appendix-b-profile-version-reference-information)中的配置文件版本后缀（.V2、.V3、.V4）改为首字母大写。 | 尽管 Windows 不区分大小写，但如果将 NFS 与文件共享配合使用，则为配置文件后缀采用正确的首字母大写（大写）形式非常重要。 |
| 2013 年 10 月 9 日 | 为 Windows Server 2012 R2 和 Windows 8.1 进行了修订，阐明了一些事项，并添加了[在多个版本的 Windows 上使用漫游用户策略文件时的注意事项](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows)和[附录 B：配置文件版本参考信息](#appendix-b-profile-version-reference-information)部分。 | 针对新版本的更新；客户反馈。 |

## <a name="more-information"></a>详细信息

- [部署文件夹重定向、脱机文件和漫游用户策略文件](deploy-folder-redirection.md)
- [为文件夹重定向以及漫游用户策略文件部署主计算机](deploy-primary-computers.md)
- [实现用户状态管理](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784645(v=ws.10)>)
- [Microsoft 关于复制的用户配置文件数据的支持声明](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
- [使用 DISM 旁加载应用](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
- [对基于 Windows 运行时的应用的打包、部署和查询进行故障排除](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)