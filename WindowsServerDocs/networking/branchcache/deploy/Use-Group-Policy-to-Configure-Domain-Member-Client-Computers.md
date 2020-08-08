---
title: 使用组策略配置域成员客户端计算机
description: 本主题是适用于 Windows Server 2016 的 BranchCache 部署指南的一部分，它演示了如何在分布式和托管缓存模式下部署 BranchCache，以优化分支机构中的 WAN 带宽使用情况
manager: dougkim
ms.topic: get-started-article
ms.assetid: 911c1538-f79d-42e9-ba38-f4618f87b008
ms.author: lizross
author: eross-msft
ms.date: 06/02/2018
ms.openlocfilehash: e36fd1b8884ea899156f2f413162efe14cce52be
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964333"
---
# <a name="use-group-policy-to-configure-domain-member-client-computers"></a>使用组策略配置域成员客户端计算机

>适用于：Windows Server（半年频道）、Windows Server 2016

在本部分中，你将为组织中的所有计算机创建一个组策略对象、使用分布式缓存模式或托管缓存模式配置域成员客户端计算机，以及配置具有高级安全性的 Windows 防火墙以允许 BranchCache 流量。

本部分包含以下过程。

1.  [创建组策略对象并配置 BranchCache 模式](#bkmk_gp)

2.  [配置具有高级安全性的 Windows 防火墙入站流量规则](#bkmk_inbound)

3.  [若要配置具有高级安全性的 Windows 防火墙出站流量规则](#bkmk_outbound)

> [!TIP]
> 在以下过程中，系统会提示你在默认域策略中创建组策略对象，但你可以在组织单位中创建对象 (OU) 或适用于你的部署的其他容器。

您必须是**Domain Admins**的成员，或者是执行这些过程的等效项。

## <a name="to-create-a-group-policy-object-and-configure-branchcache-modes"></a><a name="bkmk_gp"></a>创建组策略对象并配置 BranchCache 模式

1.  在安装了 Active Directory 域服务服务器角色的计算机上，在服务器管理器中单击 "**工具**"，然后单击**组策略管理**"。 此时会打开组策略管理控制台。

2.  在组策略管理控制台中，展开以下路径： "**林：** *example.com*"、"**域**"、" *example.com*"、"**组策略对象**"，其中 " *example.com* " 是要配置的 BranchCache 客户端计算机帐户所在的域的名称。

3.  右键单击“组策略对象”****，然后单击“新建”****。 此时将打开 "**新建 GPO** " 对话框。 在 "**名称**" 中，键入 (GPO) 的新组策略对象的名称。 例如，如果想要为对象 BranchCache 客户端计算机命名，请键入 " **Branchcache 客户端计算机**"。 单击“确定”。

4.  在组策略管理控制台中，确保选中 "**组策略对象**"，然后在 "详细信息" 窗格中，右键单击刚创建的 GPO。 例如，如果你命名了 GPO BranchCache 客户端计算机，请右键单击 " **BranchCache 客户端计算机**"。 单击 **“编辑”** 。 此时将打开组策略管理编辑器控制台。

5.  在组策略管理编辑器控制台中，展开以下路径： "**计算机配置**"、"**策略**"、"**管理模板：策略定义" (ADMX 文件) 从 "本地计算机**"、"**网络**"、" **BranchCache**" 中检索。

6.  单击 " **BranchCache**"，然后在详细信息窗格中，双击 "**启用 BranchCache**"。 此时将打开 "策略设置" 对话框。

7.  在 "**打开 BranchCache** " 对话框中，单击 "**已启用**"，然后单击 **"确定"**。

8.  若要启用 BranchCache 分布式缓存模式，请在详细信息窗格中，双击 "**设置 BranchCache 分布式缓存模式**"。 此时将打开 "策略设置" 对话框。

9. 在 "**设置 BranchCache 分布式缓存模式**" 对话框中，单击 "**已启用**"，然后单击 **"确定"**。

10. 如果你有一个或多个在托管缓存模式下部署 BranchCache 的分支机构，并且已在这些办公室中部署了托管缓存服务器，请双击 "**通过服务连接点启用自动托管缓存发现**"。 此时将打开 "策略设置" 对话框。

11. 在 "**通过服务连接点启用自动托管缓存发现**" 对话框中，单击 "**已启用**"，然后单击 **"确定"**。

    > [!NOTE]
    > 同时启用 "**设置 BranchCache 分布式缓存模式**" 和 "**通过服务连接点启用自动托管缓存发现**" 策略设置时，客户端计算机将在 BranchCache 分布式缓存模式下运行，除非它们在分支机构中查找托管缓存服务器，此时它们将在托管缓存模式下运行。

12. 使用以下过程在客户端计算机上使用组策略配置防火墙设置。

## <a name="to-configure-windows-firewall-with-advanced-security-inbound-traffic-rules"></a><a name="bkmk_inbound"></a>配置具有高级安全性的 Windows 防火墙入站流量规则

1.  在组策略管理控制台中，展开以下路径： "**林：** *example.com*"、"**域**"、" *example.com*"、"**组策略对象**"，其中 " *example.com* " 是要配置的 BranchCache 客户端计算机帐户所在的域的名称。

2.  在组策略管理控制台中，确保选中 "**组策略对象**"，然后在 "详细信息" 窗格中，右键单击之前创建的 BranchCache 客户端计算机 GPO。 例如，如果你命名了 GPO BranchCache 客户端计算机，请右键单击 " **BranchCache 客户端计算机**"。 单击 **“编辑”** 。 此时将打开组策略管理编辑器控制台。

3.  在组策略管理编辑器控制台中，展开以下路径： "**计算机配置**"、"**策略**"、" **windows 设置**"、"**安全设置**"、"**高级安全**Windows 防火墙"、"**具有高级安全性的 windows 防火墙**"、"**入站规则**"。

4.  右键单击“入站规则”****，然后单击“新建规则”****。 此时将打开 "新建入站规则向导"。

5.  在 "**规则类型**" 中，单击 "**预定义**"，展开选项列表，然后单击 " **BranchCache-内容检索" (使用 HTTP) **。 单击“下一步”。

6.  在 "**预定义规则**" 中单击 "**下一步**"。

7.  在 "**操作**" 中，确保选中 **"允许连接"** ，然后单击 "**完成**"。

    > [!IMPORTANT]
    > 你必须选择 "允许 BranchCache 客户端**的连接**才能在此端口上接收流量"。

8.  若要创建 WS-RELIABLEMESSAGING 防火墙例外，请再次右键单击 "**入站规则**"，然后单击 "**新建规则**"。 此时将打开 "新建入站规则向导"。

9. 在 "**规则类型**" 中，单击 "**预定义**"，展开选项列表，然后单击 " **BranchCache-对等发现" (使用 WSD) **。 单击“下一步”。

10. 在 "**预定义规则**" 中单击 "**下一步**"。

11. 在 "**操作**" 中，确保选中 **"允许连接"** ，然后单击 "**完成**"。

    > [!IMPORTANT]
    > 你必须选择 "允许 BranchCache 客户端**的连接**才能在此端口上接收流量"。

## <a name="to-configure-windows-firewall-with-advanced-security-outbound-traffic-rules"></a><a name="bkmk_outbound"></a>若要配置具有高级安全性的 Windows 防火墙出站流量规则

1.  在组策略管理编辑器控制台中，右键单击 "**出站规则**"，然后单击 "**新建规则**"。 此时将打开 "新建出站规则向导"。

2.  在 "**规则类型**" 中，单击 "**预定义**"，展开选项列表，然后单击 " **BranchCache-内容检索" (使用 HTTP) **。 单击“下一步”。

3.  在 "**预定义规则**" 中单击 "**下一步**"。

4.  在 "**操作**" 中，确保选中 **"允许连接"** ，然后单击 "**完成**"。

    > [!IMPORTANT]
    > 你必须选择 "允许 BranchCache 客户端**的连接**才能在此端口上发送流量"。

5.  若要创建 WS-RELIABLEMESSAGING 防火墙例外，请再次右键单击 "**出站规则**"，然后单击 "**新建规则**"。 此时将打开 "新建出站规则向导"。

6.  在 "**规则类型**" 中，单击 "**预定义**"，展开选项列表，然后单击 " **BranchCache-对等发现" (使用 WSD) **。 单击“下一步”。

7.  在 "**预定义规则**" 中单击 "**下一步**"。

8.  在 "**操作**" 中，确保选中 **"允许连接"** ，然后单击 "**完成**"。

    > [!IMPORTANT]
    > 你必须选择 "允许 BranchCache 客户端**的连接**才能在此端口上发送流量"。



