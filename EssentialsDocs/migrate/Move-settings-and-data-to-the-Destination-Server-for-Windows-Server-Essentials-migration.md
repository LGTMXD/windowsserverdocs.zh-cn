---
title: 将设置和数据移到目标服务器以进行 Windows Server Essentials 迁移
description: 描述如何使用 Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 2b882e87-347a-4010-b7fd-9599d61198dd
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a3e80eb391f913b4d62d8224afb7745eb2671289
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180533"
---
# <a name="move-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>将设置和数据移到目标服务器以进行 Windows Server Essentials 迁移

>适用于： Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

将设置和数据移到目标服务器，如下所示：：

1. [将数据复制到目标服务器](#copy-data-to-the-destination-server)

2. [配置网络](#configure-the-network)

3. [将允许的计算机映射到用户帐户](#map-permitted-computers-to-user-accounts)

## <a name="copy-data-to-the-destination-server"></a>将数据复制到目标服务器
 在将数据从源服务器复制到目标服务器之前，请执行以下任务：

- 在源服务器上查看共享文件夹列表（包括每个文件夹的权限）。 在目标服务器上创建或自定义这些文件夹，使其与要从源服务器迁移的文件夹结构相匹配。

- 查看每个文件夹的大小，并确保目标服务器具有足够的存储空间。

- 使源服务器上的共享文件夹对所有用户限制为只读，以便在将文件复制到目标服务器时，不会在驱动器上发生写入操作。

#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>将数据从源服务器复制到目标服务器

1. 以域管理员身份登录到目标服务器，然后打开一个命令窗口。

2. 在命令提示符下，键入以下命令，然后按 Enter：

 `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`

 其中：
 - \<SourceServerName\> 是源服务器的名称
 - \<SharedSourceFolderName\> 是源服务器上的共享文件夹名称
 - \<DestinationServerName\>目标服务器的名称，
 - \<SharedDestinationFolderName\>是将数据复制到的目标服务器上的共享文件夹。

3. 对每个要从源服务器迁移的共享文件夹重复上一步。

## <a name="configure-the-network"></a>配置网络
 将 DHCP 角色移到路由器之后，请在目标服务器上配置网络设置。

#### <a name="to-configure-the-network"></a>配置网络

1. 在目标服务器上，打开仪表板。

2. 在仪表板“主页”**** 页面上，单击“设置”****，单击“设置随处访问”****，然后选择“单击以配置随处访问”**** 选项。

3. 完成向导中的说明，配置你的路由器名和域名。

 如果路由器不支持 UPnP 框架，或如果 UPnP 框架已禁用，则路由器名称旁边可能会出现一个黄色的警告图标。 请确保下列端口为打开状态，并且已定向到目标服务器的 IP 地址：

- 端口 80：HTTP Web 流量

- 端口 443：HTTP Web 流量

## <a name="map-permitted-computers-to-user-accounts"></a>将允许的计算机映射到用户帐户
 从源服务器迁移的每个用户帐户都必须映射到一个或多个计算机。

#### <a name="to-map-user-accounts-to-computers"></a>将用户帐户映射到计算机

1. 打开 Windows Server Essentials 仪表板。

2. 在导航栏中，单击“用户”****。

3. 在用户帐户列表中，右键单击用户帐户，然后单击“查看帐户属性”****。

4. 单击“随处访问”**** 选项卡，然后单击”允许远程 Web 访问和访问 Web 服务应用程序”****。

5. 依次选择“共享文件夹”****、“计算机”**** 和“主页链接”****，然后单击“应用”****。

6. 单击“计算机访问”**** 选项卡，然后单击要允许访问的计算机的名称。

7. 为每个用户帐户重复步骤 3、4、5 和 6。

> [!NOTE]
> 不必更改客户端计算机的配置。 它将进行自动配置。
>
> 完成迁移后，如果你在目标服务器上创建第一个新的用户帐户时遇到问题，则请删除你已添加的用户帐户，然后再次创建它。
