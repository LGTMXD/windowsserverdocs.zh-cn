---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: 事件 ID 2088-复制成功时出现 DNS 查找失败
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f84fd7be45995e9e0b318b42c8b4152af244a9da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823050"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>事件 ID 2088：DNS 查找失败但复制成功

>适用于：Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    
    <developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
      <introduction>
    <para>When a destination domain controller running Windows Server 2003 with Service Pack 1 (SP1) receives Event ID 2088 in the Directory Service event log, attempts to resolve the globally unique identifier (GUID) in the alias (CNAME) resource record to an IP address for the source domain controller failed. However, the destination domain controller tried other means to resolve the name and succeeded by using either the fully qualified domain name (FQDN) or the NetBIOS name of the source domain controller. Although replication was successful, the Domain Name System (DNS) problem should be diagnosed and resolved. </para>
    <para>The following is an example of the event text: </para>
    <code>Log Name: Directory Service

    Source: Microsoft-Windows-ActiveDirectory_DomainService
    Date: 3/15/2008  9:20:11 AM
    Event ID: 2088
    Task Category: DS RPC Client 
    Level: Warning
    Keywords: Classic
    User: ANONYMOUS LOGON
    Computer: DC3.contoso.com
    Description:
    Active Directory could not use DNS to resolve the IP address of the 
    source domain controller listed below. To maintain the consistency 
    of Security groups, group policy, users and computers and their passwords, 
    Active Directory Domain Services successfully replicated using the NetBIOS 
    or fully qualified computer name of the source domain controller. 

无效的 DNS 配置可能会影响成员计算机、域控制器或此 Active Directory 域服务林中的应用程序服务器上的其他重要操作，包括登录身份验证或对网络资源的访问权限。 

应该立即解决此 DNS 配置错误，使此域控制器可以使用 DNS 解析源域控制器的 IP 地址。 

备用服务器名称： DC1 失败的 DNS 主机名： 4a8717eb-8e58-456c-995a-c92e4add7e8e _msdcs。 

注意：默认情况下，在任何给定的12小时时间段内只显示最多10个 DNS 故障，即使出现了10个以上的失败。  若要记录所有单独的故障事件，请将以下诊断注册表值设置为1： 

注册表路径： HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC 客户端 

用户操作： 

1) 如果源域控制器不再运行，或者已使用其他计算机名称或 NTDSDSA 对象 GUID 重新安装了其操作系统，请使用 MSKB 文章216498中所述的步骤，删除与 ntdsutil.exe 的源域控制器的元数据。 

2) 确认源域控制器正在运行 Active Directory 并且可在网络上访问，方法是键入 "net view \\&lt;源 DC 名称&gt;" 或 "ping &lt;源 DC 名称&gt;"。 

3) 验证源域控制器是否正在对 DNS 服务使用有效的 DNS 服务器，以及是否使用 DNS 增强版的 DCDIAG 正确注册了源域控制器的主机记录和 CNAME 记录。EXE 可用 <https://www.microsoft.com/dns> 

dcdiag/test： dns 

4) 通过运行 DCDIAG 的 DNS 增强版，验证此目标域控制器是否对 DNS 服务使用有效的 DNS 服务器。EXE 命令，如下所示： 

dcdiag/test： dns 

5) 有关 DNS 错误故障的进一步分析，请参阅 KB 824449： <https://support.microsoft.com/?kbid=824449> 

其他数据错误值：11004请求的名称有效，但找不到请求的类型的数据</code> </introduction>
  <section>
    <title>诊断</title>
    <content>
      <para>在 dns 中使用别名（CNAME）资源记录解决源域控制器名称失败的原因可能是 dns 的配置错误或 DNS 数据传播延迟。</para>
    </content>
  </section>
  <section>
    <title>解决方法</title>
    <content>
      <para>按照 &quot;<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">事件 ID 2087： dns 查找失败导致复制失败</link>中所述继续进行 DNS 测试。&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


