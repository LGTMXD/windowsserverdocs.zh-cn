---
title: 升级、备份和还原 SDN 基础结构
description: 本主题介绍如何更新、备份和还原 SDN 基础结构。
manager: grcusanz
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/27/2018
ms.openlocfilehash: daca883456a32c707fc2c7b9bfd6193b0d917b58
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942577"
---
# <a name="upgrade-backup-and-restore-sdn-infrastructure"></a>升级、备份和还原 SDN 基础结构

>适用于：Windows Server（半年频道）、Windows Server 2016

本主题介绍如何更新、备份和还原 SDN 基础结构。

## <a name="upgrade-the-sdn-infrastructure"></a>升级 SDN 基础结构
SDN 基础结构可以从 Windows Server 2016 升级到 Windows Server 2019。 对于升级排序，请按照 "更新 SDN 基础结构" 一节中所述的相同步骤顺序操作。 升级之前，建议对网络控制器数据库进行备份。

对于网络控制器计算机，请在升级完成后使用 NetworkControllerNode cmdlet 检查节点的状态。 在升级其他节点之前，请确保节点返回到 "Up" 状态。 升级所有网络控制器节点后，网络控制器会在一小时内更新网络控制器群集中运行的微服务。 可以使用 networkcontroller cmdlet 触发立即更新。

在软件定义的网络 (SDN) 系统的所有操作系统组件上安装相同的 Windows 更新，其中包括：

- 已启用 SDN 的 Hyper-v 主机
- 网络控制器 Vm
- 软件负载均衡器 Mux Vm
- RAS 网关 Vm

>[!IMPORTANT]
>如果你使用 System Center Virtual Manager，则必须使用最新的更新汇总来更新它。

更新每个组件时，可以使用任何标准方法来安装 Windows 更新。 但是，若要确保工作负荷的停机时间和网络控制器数据库的完整性，请遵循以下步骤：

1. 更新管理控制台。<p>在使用网络控制器 Powershell 模块的每台计算机上安装更新。  包含自行安装 NetworkController 角色的任何位置。 排除网络控制器 Vm 本身;在下一步中更新它们。

2. 在第一个网络控制器 VM 上，安装所有更新并重新启动。

3. 在继续到下一个网络控制器 VM 之前，请使用 `get-networkcontrollernode` cmdlet 检查已更新并重新启动的节点的状态。

4. 在重新启动过程中，请等待网络控制器节点关闭，然后重新打开。<p>重新启动 VM 后，可能需要几分钟时间才能进入 "**_已启动" 状态。_** 有关输出的示例，请参阅

5. 一次在每个 SLB Mux VM 上安装一个更新，以确保负载均衡器基础结构的持续可用性。

6. 更新 Hyper-v 主机和 RAS 网关，从包含处于**备用**模式的 RAS 网关的主机开始。<p>RAS 网关 Vm 不能实时迁移，且不会丢失租户连接。 在更新过程中，必须小心地将租户连接故障转移到新 RAS 网关的次数降至最低。 通过协调主机和 RAS 网关的更新，每个租户最多会进行一次故障转移。

    a. 撤走支持实时迁移的 Vm 主机。<p>RAS 网关 Vm 应保留在主机上。

    b. 在此主机上的每个网关 VM 上安装更新。

    c. 如果更新要求网关 VM 重新启动，则重新启动 VM。

    d. 在包含刚刚更新的网关 VM 的主机上安装更新。

    e. 如果更新要求，请重新启动主机。

    f. 对于包含备用网关的每个其他主机重复此步骤。<p>如果不保留备用网关，请对所有剩余主机执行相同的步骤。


### <a name="example-use-the-get-networkcontrollernode-cmdlet"></a>示例：使用 networkcontrollernode cmdlet

在此示例中，你将在 `get-networkcontrollernode` 其中一个网络控制器 vm 中查看 cmdlet 的输出。

在示例输出中看到的节点状态如下：

- NCNode1.contoso.com = Down
- NCNode2.contoso.com = Up
- NCNode3.contoso.com = Up

>[!IMPORTANT]
>你必须等待几分钟，直到节点状态在更新任何其他节点之前更改为 "_**上**_ 一次"。

更新所有网络控制器节点后，网络控制器会在一小时内更新网络控制器群集中运行的微服务。

>[!TIP]
>可以使用 cmdlet 触发立即更新 `update-networkcontroller` 。


```Powershell
PS C:\> get-networkcontrollernode
Name            : NCNode1.contoso.com
Server          : NCNode1.Contoso.com
FaultDomain     : fd:/NCNode1.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Down

Name            : NCNode2.Contoso.com
Server          : NCNode2.contoso.com
FaultDomain     : fd:/ NCNode2.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up

Name            : NCNode3.Contoso.com
Server          : NCNode3.Contoso.com
FaultDomain     : fd:/ NCNode3.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up
```

### <a name="example-use-the-update-networkcontroller-cmdlet"></a>示例：使用 networkcontroller cmdlet
在此示例中，你将看到 cmdlet 的输出，用于 `update-networkcontroller` 强制网络控制器更新。

>[!IMPORTANT]
>如果没有更多要安装的更新，请运行此 cmdlet。


```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

## <a name="backup-the-sdn-infrastructure"></a>备份 SDN 基础结构

定期备份网络控制器数据库可确保在发生灾难或数据丢失时实现业务连续性。  备份网络控制器 Vm 并不能确保会话跨多个网络控制器节点继续。

**要求：**
* 对共享和文件系统具有读/写权限的 SMB 共享和凭据。
* 如果还使用 GMSA 安装了网络控制器，则可以选择使用组托管服务帐户 (GMSA) 。

**方法**

1. 使用所选的 VM 备份方法，或使用 Hyper-v 导出每个网络控制器 VM 的副本。<p>备份网络控制器 VM 可确保存在用于对数据库进行解密的必要证书。

2. 如果使用 System Center Virtual Machine Manager (SCVMM) ，请停止 SCVMM 服务，并通过 SQL Server 将其备份。<p>此处的目标是确保在此期间不会对 SCVMM 进行任何更新，这可能会导致网络控制器备份和 SCVMM 之间出现不一致的情况。

   >[!IMPORTANT]
   >在网络控制器备份完成之前，请不要重新启动 SCVMM 服务。

3. 用 cmdlet 备份网络控制器数据库 `new-networkcontrollerbackup` 。

4. 通过 cmdlet 检查备份的完成和成功情况 `get-networkcontrollerbackup` 。

5. 如果使用 SCVMM，请启动 SCVMM 服务。



### <a name="example-backing-up-the-network-controller-database"></a>示例：备份网络控制器数据库

```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

# Get or Create Credential object for File share user

$ShareUserResourceId = "BackupUser"

$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }
If ($ShareCredential -eq $null) {
    $CredentialProperties = New-Object Microsoft.Windows.NetworkController.CredentialProperties
    $CredentialProperties.Type = "usernamePassword"
    $CredentialProperties.UserName = "contoso\alyoung"
    $CredentialProperties.Value = "<Password>"

    $ShareCredential = New-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential -Properties $CredentialProperties -ResourceId $ShareUserResourceId -Force
}

# Create backup

$BackupTime = (get-date).ToString("s").Replace(":", "_")

$BackupProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerBackupProperties
$BackupProperties.BackupPath = "\\fileshare\backups\NetworkController\$BackupTime"
$BackupProperties.Credential = $ShareCredential

$Backup = New-NetworkControllerBackup -ConnectionURI $URI -Credential $Credential -Properties $BackupProperties -ResourceId $BackupTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>示例：检查网络控制器备份操作的状态

```Powershell
PS C:\ > Get-NetworkControllerBackup -ConnectionUri $URI -Credential $Credential -ResourceId $Backup.ResourceId
| ConvertTo-JSON -Depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerBackup/2017-04-25T16_53_13",
    "InstanceId":  "c3ea75ae-2892-4e10-b26c-a2243b755dc8",
    "Etag":  "W/\"0dafea6c-39db-401b-bda5-d2885ded470e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-25T16_53_13",
    "Properties":  {
                    "BackupPath":  "\\\\fileshare\backups\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  "",
                    "FailedResourcesList":  [

                                            ],
                    "SuccessfulResourcesList":  [
                                                    "/networking/v1/credentials/11ebfc10-438c-4a96-a1ee-8a048ce675be",
                                                    "/networking/v1/credentials/41229069-85d4-4352-be85-034d0c5f4658",
                                                    "/networking/v1/credentials/b2a82c93-2583-4a1f-91f8-232b801e11bb",
                                                    "/networking/v1/credentials/BackupUser",
                                                    "/networking/v1/credentials/fd5b1b96-b302-4395-b6cd-ed9703435dd1",
                                                    "/networking/v1/virtualNetworkManager/configuration",
                                                    "/networking/v1/virtualSwitchManager/configuration",
                                                    "/networking/v1/accessControlLists/f8b97a4c-4419-481d-b757-a58483512640",
                                                    "/networking/v1/logicalnetworks/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8",
                                                    "/networking/v1/logicalnetworks/48610528-f40b-4718-938e-99c2be76f1e0",
                                                    "/networking/v1/logicalnetworks/89035b49-1ee3-438a-8d7a-f93cbae40619",
                                                    "/networking/v1/logicalnetworks/a9c8eaa0-519c-4988-acd6-11723e9efae5",
                                                    "/networking/v1/logicalnetworks/d4ea002c-c926-4c57-a178-461d5768c31f",
                                                    "/networking/v1/macPools/11111111-1111-1111-1111-111111111111",
                                                    "/networking/v1/loadBalancerManager/config",
                                                    "/networking/v1/publicIPAddresses/2c502b2d-b39a-4be1-a85a-55ef6a3a9a1d",
                                                    "/networking/v1/GatewayPools/Default",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8056-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8057-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5910-8056-b4c04f395931",
                                                    "/networking/v1/networkInterfaces/058430d3-af43-4328-a440-56540f41da50",
                                                    "/networking/v1/networkInterfaces/08756090-6d55-4dec-98d5-80c4c5a47db8",
                                                    "/networking/v1/networkInterfaces/2175d74a-aacd-44e2-80d3-03f39ea3bc5d",
                                                    "/networking/v1/networkInterfaces/2400c2c3-2291-4b0b-929c-9bb8da55851a",
                                                    "/networking/v1/networkInterfaces/4c695570-6faa-4e4d-a552-0b36ed3e0962",
                                                    "/networking/v1/networkInterfaces/7e317638-2914-42a8-a2dd-3a6d966028d6",
                                                    "/networking/v1/networkInterfaces/834e3937-f43b-4d3c-88be-d79b04e63bce",
                                                    "/networking/v1/networkInterfaces/9d668fe6-b1c6-48fc-b8b1-b3f98f47d508",
                                                    "/networking/v1/networkInterfaces/ac4650ac-c3ef-4366-96e7-d9488fb661ba",
                                                    "/networking/v1/networkInterfaces/b9f23e35-d79e-495f-a1c9-fa626b85ae13",
                                                    "/networking/v1/networkInterfaces/fdd929f1-f64f-4463-949a-77b67fe6d048",
                                                    "/networking/v1/virtualServers/15a891ee-7509-4e1d-878d-de0cb4fa35fd",
                                                    "/networking/v1/virtualServers/57416993-b410-44fd-9675-727cd4e98930",
                                                    "/networking/v1/virtualServers/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a",
                                                    "/networking/v1/virtualServers/6c812217-5931-43dc-92a8-1da3238da893",
                                                    "/networking/v1/virtualServers/d78b7fa3-812d-4011-9997-aeb5ded2b431",
                                                    "/networking/v1/virtualServers/d90820a5-635b-4016-9d6f-bf3f1e18971d",
                                                    "/networking/v1/loadBalancerMuxes/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d78b7fa3-812d-4011-9997-aeb5ded2b431_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d90820a5-635b-4016-9d6f-bf3f1e18971d_suffix",
                                                    "/networking/v1/Gateways/15a891ee-7509-4e1d-878d-de0cb4fa35fd_suffix",
                                                    "/networking/v1/Gateways/57416993-b410-44fd-9675-727cd4e98930_suffix",
                                                    "/networking/v1/Gateways/6c812217-5931-43dc-92a8-1da3238da893_suffix",
                                                    "/networking/v1/virtualNetworks/b3dbafb9-2655-433d-b47d-a0e0bbac867a",
                                                    "/networking/v1/virtualNetworks/d705968e-2dc2-48f2-a263-76c7892fb143",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.2",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.3",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.4"
                                                ],
                    "InProgressResourcesList":  [

                                                ],
                    "ProvisioningState":  "Succeeded",
                    "Credential":  {
                                        "Tags":  null,
                                        "ResourceRef":  "/credentials/BackupUser",
                                        "InstanceId":  "00000000-0000-0000-0000-000000000000",
                                        "Etag":  null,
                                        "ResourceMetadata":  null,
                                        "ResourceId":  null,
                                        "Properties":  null
                                    }
                }
}
```

## <a name="restore-the-sdn-infrastructure-from-a-backup"></a>从备份还原 SDN 基础结构

从备份中还原所有必需的组件后，SDN 环境会恢复为操作状态。

>[!IMPORTANT]
>具体步骤因还原的组件数而异。


1. 如有必要，请重新部署 Hyper-v 主机和必要的存储。

2. 如有必要，请从备份中还原网络控制器 Vm、RAS 网关 Vm 和 Mux Vm。

3. 在所有 Hyper-v 主机上停止 NC 主机代理和 SLB 主机代理：

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. 停止 RAS 网关 Vm。

5. 停止 SLB Mux Vm。

6. 用 cmdlet 还原网络控制器 `new-networkcontrollerrestore` 。

7. 检查 restore **ProvisioningState**以了解还原已成功完成的时间。

8. 如果使用 SCVMM，请使用与网络控制器备份相同的时间创建的备份来还原 SCVMM 数据库。

9. 如果要从备份还原工作负荷 Vm，请立即执行此操作。

10. 通过 networkcontrollerconfigurationstate cmdlet 检查系统的运行状况。

```Powershell
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController "https://NC.contoso.com" -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

### <a name="example-restoring-a-network-controller-database"></a>示例：还原网络控制器数据库

```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

$ShareUserResourceId = "BackupUser"
$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }

$RestoreProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerRestoreProperties
$RestoreProperties.RestorePath = "\\fileshare\backups\NetworkController\2017-04-25T16_53_13"
$RestoreProperties.Credential = $ShareCredential

$RestoreTime = (Get-Date).ToString("s").Replace(":", "_")
New-NetworkControllerRestore -ConnectionURI $URI -Credential $Credential -Properties $RestoreProperties -ResourceId $RestoreTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>示例：检查网络控制器数据库还原的状态

```PowerShell
PS C:\ > get-networkcontrollerrestore -connectionuri $uri -credential $cred -ResourceId $restoreTime | convertto-json -depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerRestore/2017-04-26T15_04_44",
    "InstanceId":  "22edecc8-a613-48ce-a74f-0418789f04f6",
    "Etag":  "W/\"f14f6b84-80a7-4b73-93b5-59a9c4b5d98e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-26T15_04_44",
    "Properties":  {
                    "RestorePath":  "\\\\sa18fs\\sa18n22\\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  null,
                    "FailedResourcesList":  null,
                    "SuccessfulResourcesList":  null,
                    "ProvisioningState":  "Succeeded",
                    "Credential":  null
                }
}
```


有关可能出现的配置状态消息的信息，请参阅[排查 Windows Server 2016 软件定义的网络堆栈问题](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)。