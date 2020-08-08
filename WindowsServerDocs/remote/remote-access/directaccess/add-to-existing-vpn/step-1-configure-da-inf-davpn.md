---
title: 步骤1配置 DirectAccess 基础结构
description: 本主题是有关 Windows Server 2016 的将 DirectAccess 添加到现有远程访问 (VPN) 部署的指南的一部分
manager: brianlic
ms.topic: article
ms.assetid: 5dc529f7-7bc3-48dd-b83d-92a09e4055c4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c52c26d44e50075f9c28dfdec7c2ab4fc420e163
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948950"
---
# <a name="step-1-configure-the-directaccess-infrastructure"></a>步骤1配置 DirectAccess 基础结构

>适用于：Windows Server（半年频道）、Windows Server 2016

本主题介绍如何配置在现有 VPN 部署中启用 DirectAccess 所需的基础结构。 在开始执行部署步骤之前，请确保已完成[步骤1：规划 DirectAccess 基础结构](Step-1-Plan-DirectAccess-Infrastructure.md)中所述的规划步骤。

|任务|描述|
|----|--------|
|配置服务器网络设置|配置远程访问服务器上的服务器网络设置。|
|配置企业网络中的路由|配置企业网络中的路由以确保正确地路由通信。|
|配置防火墙|根据需要配置其他防火墙。|
|配置 CA 和证书|启用 DirectAccess 向导将配置使用用户名和密码进行身份验证的内置 Kerberos 代理。 它还将在远程访问服务器上配置 IP-HTTPS 证书。|
|配置 DNS 服务器|配置远程访问服务器的 DirectAccess 设置。|
|配置 Active Directory|将客户端计算机加入到 Active Directory 域。|
|配置 GPO|如果必要，为部署配置 GPO。|
|配置安全组|配置将包含 DirectAccess 客户端计算机的安全组，以及部署中所需的任何其他安全组。|
|配置网络位置服务器|启用 DirectAccess 向导将在 DirectAccess 服务器上配置网络位置服务器。|

## <a name="configure-server-network-settings"></a><a name="ConfigNetworkSettings"></a>配置服务器网络设置
在使用 IPv4 和 IPv6 的环境中部署单一服务器需要下面的网络接口设置。 可使用****“Windows 网络和共享中心”中的****“更改适配器设置”配置所有 IP 地址。

-   边缘拓扑

    -   一个面向 Internet 的公共静态 IPv4 或 IPv6 地址。

    -   单个内部静态 IPv4 或 IPv6 地址。

-   在 NAT 设备后面（两个网络适配器）

    -   单个面向内部网络的静态 IPv4 或 IPv6 地址。

-   在 NAT 设备后面（一个网络适配器）

    -   单个静态 IPv4 或 IPv6 地址。

> [!NOTE]
> 如果远程访问服务器具有两个网络适配器（一个归类于域配置文件，另一个归类于公钥/私钥配置文件），但使用单一的 NIC 拓扑，则推荐的方法如下所示：
>
> 1.  确保第 2 个 NIC 也归类于域配置文件（推荐）。
> 2.  如果出于任何原因，不能为域配置文件配置第 2 个 NIC，则必须使用以下 Windows PowerShell 命令手动将 DirectAccess IPsec 策略的作用域覆盖到所有配置文件：
>
>     ```
>     $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>
>     Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any
>     Save-NetGPO -GPOSession $gposession
>     ```

## <a name="configure-routing-in-the-corporate-network"></a><a name="ConfigRouting"></a>配置企业网络中的路由
在企业网络中配置路由，如下所示：

-   在组织中部署本机 IPv6 时，添加一个路由，以便内部网络上的路由器通过远程访问服务器将 IPv6 通信路由回来。

-   在远程访问服务器上手动配置组织 IPv4 和 IPv6 路由。 添加已发布的路由，以便将所有具有组织 (/48) IPv6 前缀的通信都转发到内部网络。 此外，对于 IPv4 通信，请添加显式路由，以便将 IPv4 通信转发到内部网络。

## <a name="configure-firewalls"></a><a name="ConfigFirewalls"></a>配置防火墙
在部署中使用其他防火墙的情况下，当远程访问服务器位于 IPv4 Internet 上时，应用远程访问通信的以下面向 Internet 的防火墙例外情况：

-   6to4 流量-IP 协议41入站和出站。

-   Ip-https-传输控制协议 (TCP) 目标端口443和 TCP 源端口443出站。 当远程访问服务器配有单一网络适配器，且网络位置服务器位于远程访问服务器上时，还需要 TCP 端口 62000。

在使用其他防火墙的情况下，当远程访问服务器位于 IPv6 Internet 上时，应用远程访问通信的以下面向 Internet 的防火墙例外：

-   IP 协议 50

-   UDP 目标端口 500 入站，以及 UDP 源端口 500 出站。

当使用其它防火墙时，应用远程访问通信的以下内部网络防火墙例外情况：

-   ISATAP-协议41入站和出站

-   所有 IPv4/IPv6 通信的 TCP/UDP

## <a name="configure-cas-and-certificates"></a><a name="ConfigCAs"></a>配置 CA 和证书
启用 DirectAccess 向导将配置使用用户名和密码进行身份验证的内置 Kerberos 代理。 它还将在远程访问服务器上配置 IP-HTTPS 证书。

### <a name="configure-certificate-templates"></a><a name="ConfigCertTemp"></a>配置证书模板
当你使用内部 CA 颁发证书时，必须为 IP-HTTPS 证书和网络位置服务器网站证书配置证书模板。

##### <a name="to-configure-a-certificate-template"></a>配置证书模板的步骤

1.  在内部 CA 中，根据 [创建证书模板](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731705(v=ws.10))中所述创建一个证书模板。

2.  根据 [部署证书模板](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770794(v=ws.10))中所述部署该证书模板。

### <a name="configure-the-ip-https-certificate"></a>配置 IP-HTTPS 证书
远程访问需要使用 IP-HTTPS 证书对到远程访问服务器的 IP-HTTPS 连接进行身份验证。 有三个 IP-HTTPS 证书的证书选项：

-   **公开**-由第三方提供。

    用于 IP-HTTPS 身份验证的证书。 如果证书使用者名称不是通配符，则它必须是仅用于远程访问服务器 IP-HTTPS 连接的可从外部解析的 FQDN URL。

-   **Private**-需要以下项（如果它们尚不存在）：

    -   用于 IP-HTTPS 身份验证的网站证书。 证书使用者应该是可从 Internet 访问且可从外部解析的完全限定的域名 (FQDN)。

    -   能够从可公开解析的 FQDN 访问的证书吊销列表 (CRL) 分发点。

-   **自签名**-以下是必需的（如果它们尚不存在）：

    > [!NOTE]
    > 无法在多站点部署中使用自签名证书。

    -   用于 IP-HTTPS 身份验证的网站证书。 证书使用者应该是可从 Internet 访问且可从外部解析的 FQDN。

    -   能够从可公开解析的完全限定的域名 (FQDN) 访问的 CRL 分发点。

确保用于 IP-HTTPS 身份验证的网站证书符合以下要求：

-   该证书的公用名应与 IP-HTTPS 站点的名称相匹配。

-   在“使用者”字段中，指定远程访问服务器面向外部适配器的 IPv4 地址，或 IP-HTTPS URL 的 FQDN。

-   对于“增强型密钥使用”字段，请使用服务器身份验证对象标识符 (OID)。

-   对于“CRL 分发点”字段，请指定已连接到 Internet 的 DirectAccess 客户端可访问的 CRL 分发点。

-   IP-HTTPS 证书必须包含私钥。

-   必须直接将 IP-HTTPS 证书导入到个人存储中。

-   IP-HTTPS 证书的名称中可以包含通配符。

##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>安装内部 CA 颁发的 IP-HTTPS 证书

1.  在远程访问服务器上：在 "**开始**" 屏幕上，键入**mmc.exe**，然后按 enter。

2.  在 MMC 控制台的“文件”菜单上，单击“添加/删除管理单元”。

3.  在****“添加或删除管理单元”对话框上，依次单击****“证书”、****“添加”、****“计算机帐户”、****“下一步”、****“本地计算机”和****“完成”，然后单击****“确定”。

4.  在证书管理单元的控制台树中，依次打开****“证书(本地计算机)\个人\证书”。

5.  右键单击****“证书”，指向****“所有任务”，然后单击****“申请新证书”。

6.  单击“下一步”**** 两次。

7.  在 "**申请证书**" 页上，选中证书模板对应的复选框，如果需要，请单击 "**注册此证书需要详细信息**"。

8.  在****“证书属性”对话框的****“使用者”选项卡上，在****“使用者名称”区域的****“类型”中选择****“公用名”。

9. 在****“值”中，指定远程访问服务器面向外部的适配器的 IPv4 地址，或 IP-HTTPS URL 的 FQDN，然后单击****“添加”。

10. 在****“备用名称”区域的****“类型”中，选择****“DNS”。

11. 在****“值”中，指定远程访问服务器面向外部的适配器的 IPv4 地址，或 IP-HTTPS URL 的 FQDN，然后单击****“添加”。

12. 在****“常规”选项卡的****“友好名称”中，输入一个有助于标识证书的名称。

13. 在“扩展”**** 选项卡上，单击“扩展密钥用法”**** 旁边的箭头，并确保“服务器身份验证”出现在“已选选项”**** 列表中。

14. 依次单击****“确定”、****“注册”和****“完成”。

15. 在证书管理单元的详细信息窗格中，通过“服务器身份验证的预期目的”验证是否注册了新证书。

## <a name="configure-the-dns-server"></a><a name="ConfigDNS"></a>配置 DNS 服务器
你必须为部署中的内部网络手动配置用于网络位置服务器网站的 DNS 条目。

### <a name="to-create-the-network-location-server-and-web-probe-dns-records"></a><a name="NLS_DNS"></a>创建网络位置服务器和 Web 探测 DNS 记录

1.  在 "内部网络 DNS 服务器：" 的 "**开始**" 屏幕上，键入 * * dnsmgmt.msc * *，然后按 enter。

2.  在****“DNS 管理器”控制台的左窗格中，展开域的前向查找区域。 右键单击该域，然后单击****“新建主机(A 或 AAAA)”。

3.  在“新主机”**** 对话框的“名称(如果为空则使用父域名)”**** 框中，输入网络位置服务器网站的 DNS 名称（这是 DirectAccess 客户端用于连接到网络位置服务器的名称）。 在“IP 地址”**** 框中，输入网络位置服务器的 IPv4 地址，然后单击“添加主机”****。 在“DNS”**** 对话框中，单击“确定”****。

4.  在“新主机”**** 对话框的“名称(如果为空则使用父域名)”**** 框中，输入 Web 探测的 DNS 名称（默认 Web 探测的名称为 directaccess-webprobehost）。 在****“IP 地址”框中，输入 Web 探测的 IPv4 地址，然后单击“添加主机”****。 为 directaccess corpconnectivityhost 和任何手动创建的连接性验证程序重复此过程。 在“DNS”**** 对话框中，单击“确定”****。

5.  单击“Done”（完成） 。

![Windows PowerShell](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)***<em>windows powershell 等效命令</em>***

下面一个或多个 Windows PowerShell cmdlet 执行的功能与前面的过程相同。 在同一行输入每个 cmdlet（即使此处可能因格式限制而出现多行换行）。

```
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>
```

还必须为以下内容配置 DNS 条目：

-   Ip-https**服务器**-DirectAccess 客户端必须能够从 Internet 解析远程访问服务器的 DNS 名称。

-   **CRL 吊销检查**-directaccess 使用证书吊销检查来检查 directaccess 客户端与远程访问服务器之间的 ip-https 连接，以及 directaccess 客户端和网络位置服务器之间基于 HTTPS 的连接。 在这两种情况下，DirectAccess 客户端都必须能够解析和访问 CRL 分发点位置。

## <a name="configure-active-directory"></a><a name="ConfigAD"></a>配置 Active Directory
必须将远程访问服务器和所有 DirectAccess 客户端计算机都加入 Active Directory 域。 DirectAccess 客户端计算机必须是以下域类型之一的成员：

-   与远程访问服务器属于同一林的域。

-   属于与远程访问服务器林具有双向信任关系的林的域。

-   与远程访问服务器域具有双向域信任的域。

#### <a name="to-join-client-computers-to-the-domain"></a>将客户端计算机加入域

1.  在 "**开始**" 屏幕上，键入**explorer.exe**，然后按 enter。

2.  右键单击计算机图标，然后单击“属性”****。

3.  在****“系统”页上，单击****“高级系统设置”。

4.  在 **“系统属性”** 对话框上的 **“计算机名称”** 选项卡上，单击 **“更改”**。

5.  如果在将服务器加入域时还要更改计算机名，请在“计算机名”中键入计算机的名称****。 在“隶属于”下面单击“域”，键入服务器要加入到的域的名称（例如 corp.contoso.com），然后单击“确定”************。

6.  当系统提示你输入用户名和密码时，请输入有权将计算机加入域的用户的用户名和密码，然后单击“确定”****。

7.  当你看到欢迎你进入域的对话框时，请单击“确定”****。

8.  当系统提示你必须重新启动计算机时，请单击“确定”****。

9. 在“系统属性”**** 对话框中单击“关闭”。 出现提示时单击“立即重新启动”****。

![Windows PowerShell](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)***<em>windows powershell 等效命令</em>***

下面一个或多个 Windows PowerShell cmdlet 执行的功能与前面的过程相同。 在同一行输入每个 cmdlet（即使此处可能因格式限制而出现多行换行）。

注意：输入下面的“Add-Computer”命令后，你必须提供域凭据。

```
Add-Computer -DomainName <domain_name>
Restart-Computer
```

## <a name="configure-gpos"></a><a name="ConfigGPOs"></a>配置 GPO
若要部署远程访问，需要至少两个组策略对象：一个组策略对象包含远程访问服务器的设置，另一个包含 DirectAccess 客户端计算机的设置。 配置远程访问时，向导将自动创建所需的组策略对象。 但是，如果你的组织强制使用命名约定，或者你没有创建或编辑组策略对象所需的权限，则必须在配置远程访问之前创建它们。

若要创建组策略对象，请参阅[创建和编辑组策略对象](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754740(v=ws.11))。

> [!IMPORTANT]
> 管理员可以使用以下步骤手动将 DirectAccess 组策略对象链接到组织单位：
>
> 1.  在配置 DirectAccess 之前，请将已创建的 GPO 链接到各自的组织单位。
> 2.  要配置 DirectAccess，请为客户端计算机指定安全组。
> 3.  远程访问管理员不一定具有将组策略对象链接到域的权限。 在任一情况下，都将自动配置组策略对象。 如果已将 GPO 链接到 OU，则将不会删除这些链接，并且不会将 GPO 链接到域。 对于服务器 GPO，OU 必须包含该服务器计算机对象，否则该 GPO 将链接到域的根。
> 4.  如果在运行 DirectAccess 向导之前尚未完成链接到 OU 的链接，则在配置完成后，域管理员可以将 DirectAccess 组策略对象链接到所需的组织单位。 可以删除指向域的链接。 可在[此处](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732979(v=ws.11))找到将组策略对象链接到组织单位的步骤。

> [!NOTE]
> 如果组策略对象手动创建，则在 DirectAccess 配置过程中，组策略对象将不可用。 可能没有将组策略对象复制到最接近管理计算机的域控制器。 在这种情况下，管理员可以等待复制完成，或者强制进行复制。

## <a name="configure-security-groups"></a><a name="ConfigSGs"></a>配置安全组
客户端计算机组策略对象中包含的 DirectAccess 设置仅应用于配置远程访问时指定的安全组成员的计算机。 此外，如果要使用安全组管理应用程序服务器，则为这些服务器创建安全组。

### <a name="to-create-a-security-group-for-directaccess-clients"></a><a name="Sec_Group"></a>为 DirectAccess 客户端创建安全组

1.  在 "**开始**" 屏幕上，键入**dsa.msc**，然后按 enter。 在****“Active Directory 用户和计算机”控制台的左窗格中，展开将包含安全组的域，右键单击****“用户”，指向****“新建”，然后单击****“组”。

2.  在****“新建对象 – 组”对话框中的****“组名”下，输入该安全组的名称。

3.  在****“组范围”下单击****“全局”，在****“组类型”下单击“安全”****，然后单击“确定”****。

4.  双击 DirectAccess 客户端计算机安全组，然后在属性对话框中，单击****“成员”选项卡。

5.  在“成员”**** 选项卡上，单击“添加”****。

6.  在****“选择用户、联系人、计算机或服务帐户”对话框中，选择你希望为 DirectAccess 启用的客户端计算机，然后单击****“确定”。

![Windows PowerShell](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)**Windows powershell 等效命令**

下面一个或多个 Windows PowerShell cmdlet 执行的功能与前面的过程相同。 在同一行输入每个 cmdlet（即使此处可能因格式限制而出现多行换行）。

```
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>
```

## <a name="configure-the-network-location-server"></a><a name="ConfigNLS"></a>配置网络位置服务器
网络位置服务器应该位于高可用性服务器上，它应具有 DirectAccess 客户端信任的有效 SSL 证书。 对于网络位置服务器证书而言，存在两种证书选择：

-   **Private**-需要以下项（如果它们尚不存在）：

    -   用于网络位置服务器的网站证书。 证书使用者应该是网络位置服务器的 URL。

    -   在内部网络中高度可用的 CRL 分发点。

-   **自签名**-以下是必需的（如果它们尚不存在）：

    > [!NOTE]
    > 无法在多站点部署中使用自签名证书。

    -   用于网络位置服务器的网站证书。 证书使用者应该是网络位置服务器的 URL。

> [!NOTE]
> 如果网络位置服务器网站位于远程访问服务器上，则在配置绑定到你提供的服务器证书的远程访问时，将自动创建一个网站。

#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>安装内部 CA 颁发的网络位置服务器证书

1.  在将托管网络位置服务器网站的服务器上：在 "**开始**" 屏幕上，键入**mmc.exe**，然后按 enter。

2.  在 MMC 控制台的“文件”菜单上，单击“添加/删除管理单元”。

3.  在****“添加或删除管理单元”对话框上，依次单击****“证书”、****“添加”、****“计算机帐户”、****“下一步”、****“本地计算机”和****“完成”，然后单击****“确定”。

4.  在证书管理单元的控制台树中，依次打开****“证书(本地计算机)\个人\证书”。

5.  右键单击****“证书”，指向****“所有任务”，然后单击****“申请新证书”。

6.  单击“下一步”**** 两次。

7.  在 "**申请证书**" 页上，选中证书模板对应的复选框，如果需要，请单击 "**注册此证书需要详细信息**"。

8.  在****“证书属性”对话框的****“使用者”选项卡上，在****“使用者名称”区域的****“类型”中选择****“公用名”。

9. 在****“值”中，输入网络位置服务器网站的 FQDN，然后单击****“添加”。

10. 在****“备用名称”区域的****“类型”中，选择****“DNS”。

11. 在****“值”中，输入网络位置服务器网站的 FQDN，然后单击****“添加”。

12. 在****“常规”选项卡的****“友好名称”中，输入一个有助于标识证书的名称。

13. 依次单击****“确定”、****“注册”和****“完成”。

14. 在证书管理单元的详细信息窗格中，通过“服务器身份验证的预期目的”验证是否注册了新证书。



