---
title: 管理 Active Directory 管理中心中的不同域
description: Windows Server 安全
ms.prod: windows-server
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6690ffbc558db4026c3fe67168907ca953ad4081
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856980"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>管理 Active Directory 管理中心中的不同域

>适用于：Windows Server（半年频道）、Windows Server 2016

  当你打开 Active Directory 管理 "时，你当前登录到此计算机上的域将 \(本地域\) 出现在 Active Directory 管理中心导航窗格中 \(左窗格\)。 根据当前登录凭据集的权限，你可以查看或管理本地域中的 Active Directory 对象。

 你还可以使用相同的一组登录凭据和 Active Directory 管理中心的同一个实例来查看或管理同一林中的任何其他域中的 Active Directory 对象或与本地域建立了信任关系的另一个林中的域。 同时支持两种\-方式信任和两种\-的信任。

> [!NOTE]
>  如果域 a 和域 B 之间存在一种\-方式信任，域 A 中的用户可以访问域 B 中的资源，但是域 B 中的用户无法访问域 A 中的资源，如果在域 A 所属的计算机上运行 Active Directory 管理中心，则可以使用当前的一组登录凭据和在同一 Active Directory 管理中心实例中连接到域 B。 但如果在域 B 是本地域的计算机上运行 Active Directory 管理中心，则无法使用同一 Active Directory 管理中心实例中的相同凭据集连接到域 A。

 不需要任何最低组成员身份即可完成此过程。

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012：使用当前登录凭据集在所选实例中管理外域 Active Directory 管理中心

1.  若要打开 Active Directory 管理中心，请在**服务器管理器**中单击 "**工具**"，然后单击 " **Active Directory 管理中心**"。

    > [!NOTE]
    >  打开 Active Directory 管理中心的另一种方法是单击 "**开始**"，然后键入**dsac.exe**。

2.  若要打开 "**添加导航节点**"，请单击 "**管理**"，然后单击 "**添加导航节点**"，如下图所示。

     ![显示 * * 添加导航节点的屏幕截图 * * UI](media/ADDS_ADACAddNavNode.gif)

3.  在 "**添加导航节点**" 中，单击 "**连接到其他域**"，如下图所示。

     ![显示 * * 添加导航节点的屏幕截图 * * UI](media/ADDS_ADACConnectToDomain.gif)

4.  在 "**连接到**" 中，键入要管理的外部域的名称 \(例如**contoso.com**\)，然后单击 **"确定"** 。

5.  成功连接到外部域后，浏览 "**添加导航节点**" 窗口中的列，选择要添加到 Active Directory 管理中心导航窗格中的容器，然后单击 **"确定"** 。

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2：使用当前登录凭据集在所选实例中管理外域 Active Directory 管理中心

1. 若要打开 Active Directory 管理中心，请单击 "**开始**"，单击 "**管理工具**"，然后单击 " **Active Directory 管理中心**"。

   > [!NOTE]
   >  打开 Active Directory 管理中心的另一种方法是单击 "**开始**"，再单击 "**运行**"，然后键入**dsac.exe**。

2. 若要打开 "**添加导航节点**"，在 "Active Directory 管理中心" 窗口顶部附近，单击 "**添加导航节点**"，如下图所示。

    ![显示 * * 添加导航节点的屏幕截图 * * UI](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  打开 "**添加导航节点**" 的另一种方法是右\-单击 Active Directory 管理中心导航窗格中的空白区域中的任意位置，然后单击 "**添加导航节点**"。

3. 在 "**添加导航节点**" 中，单击 "**连接到其他域**"，如下图所示。

    ![显示 * * 添加导航节点的屏幕截图 * * * 连接到其他域 * * UI](media/add_nav_nodes.gif)

4. 在 "**连接到**" 中，键入要管理的外部域的名称 \(例如**contoso.com**\)，然后单击 **"确定"** 。

5. 成功连接到外部域后，浏览 "**添加导航节点**" 窗口中的列，选择要添加到 Active Directory 管理中心导航窗格中的容器，然后单击 **"确定"** 。

   有关自定义 Active Directory 管理中心导航窗格的详细信息，请参阅[自定义 Active Directory 管理中心导航窗格](customize-the-active-directory-administrative-center-navigation-pane.md)。

   你还可以通过使用一组不同于当前登录凭据集的登录凭据来打开 Active Directory 管理中心。 如果你使用普通用户凭据登录到运行 Active Directory 管理中心的计算机，但你想要在此计算机上使用 Active Directory 管理中心来以管理员身份管理本地域，则以下过程中的命令可能非常有用。 如果你想要使用 Active Directory 管理中心以远程方式管理与你的本地域不同的外域，并使用与当前登录凭据集不同的一组凭据，\(此命令也会很有用。 但是，外部域必须与本地域建立了信任关系。\)

   不需要任何最低组成员身份即可完成此过程。

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>使用与当前登录凭据集不同的登录凭据管理域的步骤

1.  若要打开 Active Directory 管理中心，请在命令提示符下键入以下命令，然后按 ENTER：

     `runas /user:<domain\user> dsac`

     其中 `<domain\user>` 是要打开 Active Directory 管理中心的凭据集，`dsac` 是 \(Dsac.exe\)的 Active Directory 管理中心可执行文件名称。

     例如，键入以下命令，然后按 Enter：

     `runas /user:contoso\administrator dsac`

2.  打开 Active Directory 管理中心后，浏览导航窗格来查看或管理 Active Directory 域。

  

