---
title: 在 Windows 10 中配置 VPN 设备隧道
description: 了解如何在 Windows 10 中创建 VPN 设备隧道。
ms.date: 11/05/2018
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 04500e2a9d5623aa9ce9796088bda2e4a6a5eccd
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996787"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>在 Windows 10 中配置 VPN 设备隧道

>适用于： Windows 10 版本1709

Always On VPN 使你能够为设备或计算机创建专用 VPN 配置文件。 Always On VPN 连接包括两种隧道：

- _设备隧道_在用户登录到设备之前连接到指定的 VPN 服务器。 预登录连接方案和设备管理将使用设备隧道。

- _用户隧道_仅在用户登录到设备后进行连接。 用户隧道允许用户通过 VPN 服务器访问组织资源。

与仅在用户登录到设备或计算机之后进行连接的_用户隧道_不同，_设备隧道_允许 VPN 在用户登录之前建立连接。 _设备隧道_和_用户隧道_独立操作其 VPN 配置文件，可以同时连接，并且可以根据需要使用不同的身份验证方法和其他 VPN 配置设置。 用户隧道支持 SSTP 和 IKEv2，而设备隧道仅支持 IKEv2，而不支持 SSTP 回退。

在已加入域、未加入域的 (工作组) 或 Azure AD 加入设备上，支持企业和 BYOD 方案的用户隧道。 它可在所有 Windows 版本中使用，并且平台功能可通过 UWP VPN 插件支持的方式提供给第三方。

只能在运行 Windows 10 企业版或教育版1709或更高版本的已加入域的设备上配置设备隧道。 不支持第三方控制设备隧道。 设备隧道不支持使用名称解析策略表 (NRPT) 。 设备隧道不支持强制隧道。 您必须将其配置为拆分隧道。


## <a name="device-tunnel-requirements-and-features"></a>设备隧道要求和功能
必须启用 VPN 连接的计算机证书身份验证，并定义根证书颁发机构来验证传入的 VPN 连接。

```PowerShell
$VPNRootCertAuthority = "Common Name of trusted root certification authority"
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like "*$VPNRootCertAuthority*" })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![设备隧道功能和要求](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>VPN 设备隧道配置

下面的示例配置文件 XML 为仅要求客户端发起的请求通过设备隧道的情况提供了良好的指南。  将利用流量筛选器将设备隧道限制为仅管理流量。  此配置适用于 Windows 更新、典型的组策略 (GP) 和 Microsoft Endpoint Configuration Manager 更新方案，以及用于首次登录而没有缓存凭据的 VPN 连接，或密码重置方案。

对于服务器启动的推送案例（如 Windows 远程管理 (WinRM) 、远程 GPUpdate 和远程 Configuration Manager 更新方案），必须允许设备隧道上的入站流量，因此无法使用流量筛选器。  如果在设备隧道配置文件中打开流量筛选器，则设备隧道将拒绝入站流量。  此限制将在未来版本中删除。


### <a name="sample-vpn-profilexml"></a>示例 VPN profileXML

下面是示例 VPN profileXML。

``` xml
<VPNProfile>
  <NativeProfile>
<Servers>vpn.contoso.com</Servers>
<NativeProtocolType>IKEv2</NativeProtocolType>
<Authentication>
  <MachineMethod>Certificate</MachineMethod>
</Authentication>
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
 <!-- disable the addition of a class based route for the assigned IP address on the VPN interface -->
<DisableClassBasedDefaultRoute>true</DisableClassBasedDefaultRoute>
  </NativeProfile>
  <!-- use host routes(/32) to prevent routing conflicts -->
  <Route>
<Address>10.10.0.2</Address>
<PrefixSize>32</PrefixSize>
  </Route>
  <Route>
<Address>10.10.0.3</Address>
<PrefixSize>32</PrefixSize>
  </Route>
<!-- traffic filters for the routes specified above so that only this traffic can go over the device tunnel -->
  <TrafficFilter>
<RemoteAddressRanges>10.10.0.2, 10.10.0.3</RemoteAddressRanges>
  </TrafficFilter>
<!-- need to specify always on = true -->
  <AlwaysOn>true</AlwaysOn>
<!-- new node to specify that this is a device tunnel -->
 <DeviceTunnel>true</DeviceTunnel>
<!--new node to register client IP address in DNS to enable manage out -->
<RegisterDNS>true</RegisterDNS>
</VPNProfile>
```

根据每个特定部署方案的需求，可通过设备隧道配置的其他 VPN 功能是[受信任的网络检测](/answers/topics/windows-server-infrastructure.html)。

```
 <!-- inside/outside detection -->
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

## <a name="deployment-and-testing"></a>部署和测试

可以使用 Windows PowerShell 脚本并使用 Windows Management Instrumentation (WMI) bridge 来配置设备隧道。 必须在**本地系统**帐户的上下文中配置 Always On VPN 设备隧道。 若要实现此目的，需要使用[PsExec](/sysinternals/downloads/psexec)，这是[Sysinternals](/sysinternals/)套件中包含的其中一个[PsTools](/sysinternals/downloads/pstools) 。

有关如何部署每个设备 `(.\Device)` 和每个用户配置文件的指南 `(.\User)` ，请参阅将[POWERSHELL 脚本与 WMI 桥接程序结合使用](/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider)。

运行以下 Windows PowerShell 命令，以验证是否已成功部署设备配置文件：

  ```powershell
  Get-VpnConnection -AllUserConnection
  ```

输出显示在 \- 设备上部署的设备范围 VPN 配置文件的列表。

### <a name="example-windows-powershell-script"></a>Windows PowerShell 脚本示例

你可以使用以下 Windows PowerShell 脚本来帮助创建你自己的用于创建配置文件的脚本。

```PowerShell
Param(
[string]$xmlFilePath,
[string]$ProfileName
)

$a = Test-Path $xmlFilePath
echo $a

$ProfileXML = Get-Content $xmlFilePath

echo $XML

$ProfileNameEscaped = $ProfileName -replace ' ', '%20'

$Version = 201606090004

$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'

$nodeCSPURI = './Vendor/MSFT/VPNv2'
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"

$session = New-CimSession

try
{
$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", 'String', 'Property')
$newInstance.CimInstanceProperties.Add($property)

$session.CreateInstance($namespaceName, $newInstance)
$Message = "Created $ProfileName profile."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}
$Message = "Complete."
Write-Host "$Message"
```

## <a name="additional-resources"></a>其他资源

下面是帮助你进行 VPN 部署的其他资源。

### <a name="vpn-client-configuration-resources"></a>VPN 客户端配置资源

以下是 VPN 客户端配置资源。

- [如何在 Configuration Manager 中创建 VPN 配置文件](/configmgr/protect/deploy-use/create-vpn-profiles)
- [配置 Windows 10 客户端 Always On VPN 连接](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN 配置文件选项](/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-gateway-resources"></a>远程访问服务器网关资源

以下是远程访问服务器 (RAS) 的网关资源。

- [使用计算机身份验证证书配置 RRAS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd458982(v=ws.11))
- [IKEv2 VPN 连接疑难解答](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd941612(v=ws.10))
- [配置基于 IKEv2 的远程访问](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff687731(v=ws.10))

>[!IMPORTANT]
>将设备隧道与 Microsoft RAS 网关结合使用时，你需要将 RRAS 服务器配置为支持 IKEv2 计算机证书身份验证，方法是为 IKEv2 身份验证方法启用 "**允许计算机证书身份验证**"，如[此处](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ee922682%28v=ws.10%29)所述。 启用此设置后，强烈建议**将 VpnAuthProtocol** PowerShell Cmdlet 与**RootCertificateNameToAccept**可选参数一起使用，以确保 RRAS IKEv2 连接仅适用于链接到显式定义的内部/专用根证书颁发机构的 VPN 客户端证书。 另外，应修改 RRAS 服务器上**受信任的根证书颁发机构**存储，以确保它不包含[本文](/archive/blogs/rrasblog/what-type-of-certificate-to-install-on-the-vpn-server)中所述的公共证书颁发机构。 其他 VPN 网关可能还需要考虑类似的方法。