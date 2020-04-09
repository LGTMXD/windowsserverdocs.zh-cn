---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: 为联合服务器代理角色配置计算机
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: a8bfe21f50a68edfcdbc7c937dc914ff1e1d94c3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854900"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>为联合服务器代理角色配置计算机

使用所需证书配置计算机并安装联合身份验证服务代理角色服务后，你就可以将计算机配置为联合服务器代理。 可以使用以下过程，使计算机承担联合服务器代理角色。  
  
> [!IMPORTANT]  
> 在使用此过程配置联合服务器代理计算机之前，请确保已按照清单中的所有步骤进行操作：按照列出的顺序[设置联合服务器代理](Checklist--Setting-Up-a-Federation-Server-Proxy.md)。 确保至少部署一台联合服务器，并且实施了用于对联合服务器代理配置进行授权的所有必需凭据。 还必须在默认网站上配置安全套接字层 \(SSL\) 绑定，否则此向导将不会启动。 必须先完成所有这些任务，然后此联合服务器代理才可正常工作。  
  
完成设置计算机之后，验证联合服务器代理按预期方式工作。 有关详细信息，请参阅[验证联合服务器代理是否正常运行](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)。  
  
若要完成此过程，至少需要是本地计算机上的**管理员**组或等效组中的成员。  可在[本地默认组和域默认组](https://go.microsoft.com/fwlink/?LinkId=83477)中查看有关使用适合的帐户和组成员身份的详细信息。   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>配置承担联合服务器代理角色的计算机  
  
1.  可通过两种方法启动 AD FS 联合服务器配置向导。 若要启动该向导，可执行以下操作之一：  
  
    -   在 "**开始**" 屏幕上，键入 "**AD FS 联合服务器代理配置向导**"，然后按 enter。  
  
    -   安装向导完成后，请打开 Windows 资源管理器，导航到**C：\\Windows\\ADFS**文件夹，然后\-双击 " **fspconfigwizard.exe**"。  
  
2.  使用任一方法启动向导，然后在 **“欢迎”** 页上单击 **“下一步”** 。  
  
3.  在 **“指定联合身份验证服务名称”** 页的 **“联合身份验证服务名称”** 下，键入表示此计算机要充当其代理角色的联合身份验证服务的名称。  
  
4.  根据你的特定网络要求，确定你是否需要使用 HTTP 代理服务器将请求转发到联合身份验证服务。 如果是，请选中 **“向此联合身份验证服务发送请求时使用 HTTP 代理服务器”** 复选框，在 **“HTTP 代理服务器地址”** 下键入代理服务器的地址，单击 **“测试连接”** 以验证连接，然后单击 **“下一步”** 。  
  
5.  当系统提示时，指定在此联合服务器代理与联合身份验证服务之间建立信任所需的凭据。  
  
    默认情况下，只有联合身份验证服务或本地内置\\管理员组的成员才能授权联合服务器代理。  
  
6.  在 **“准备应用设置”** 页上复查详细信息。 如果设置看上去没有问题，请单击 **“下一步”** ，以开始使用这些代理设置配置此计算机。  
  
7.  在 **“配置结果”** 页上复查结果。 完成所有配置步骤后，单击“关闭”  以退出向导。  
  
    没有 Microsoft 管理控制台 \(MMC\) 管理联合服务器代理中的\-。 若要为组织中的每个联合服务器代理配置设置，请使用 Windows PowerShell cmdlet。  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>为代理操作配置备用 TCP\/IP 端口  
默认情况下，联合服务器代理服务配置为使用 TCP 端口443进行 HTTPS 通信，并将端口80用于 HTTP 流量，以便与联合服务器通信。 若要配置不同的端口，例如对应 HTTPS 的 TCP 端口 444 和对应 HTTP 的端口 81，则必须完成以下任务。  
  
> [!NOTE]  
> 如果打算在备用 TCP\/IP 端口下部署 AD FS 来操作，应该首先在联合服务器和联合服务器代理计算机上的 HTTP 和 HTTPS 的 IIS 协议绑定中修改端口。 这应该在运行用于初始配置的 AD FS 配置向导之前发生。 如果将 Internet Information Services 配置 \(首先 IIS\)，则在\-中发生向导 AD FS 配置时，将会发现备用 TCP\/IP 端口设置，并且不需要执行以下过程。 如果你想要以后更改端口设置，应首先更新 IIS 协议绑定，然后使用以下过程来相应地更新端口设置。 有关编辑 IIS 绑定的详细信息，请参阅 Microsoft 知识库中的[文章 149605](https://go.microsoft.com/fwlink/?LinkId=190275) 。  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>配置要使用的联合服务器代理的备用 TCP\/IP 端口  
  
1.  配置联合服务器以使用非默认端口。  
  
    为此，请通过将 " *HttpsPort* " 和 " *HttpPort* " 选项作为**Set\-set-adfsproperties** cmdlet 的一部分，来指定非默认端口号。 例如，若要配置这些端口，请在联合服务器计算机上的 Windows PowerShell 会话中使用以下命令：  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  将联合服务器代理配置为使用非默认端口。  
  
    为此，请通过将 " *HttpsPort* " 和 " *HttpPort* " 选项作为**Set\-ADFSProxyProperties** cmdlet 的一部分，来指定非默认端口号。 例如，若要配置这些端口，请在联合服务器计算机上的 Windows PowerShell 会话中使用以下命令：  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > 默认情况下，不会为联合服务器代理服务启用终结点 Url。 如果要配置新的联合服务器安装，则必须首先启用联合服务器代理服务终结点。 例如，假设对于本过程中的示例所引用的所有终结点，通过在中的 AD FS 管理 "管理单元\-中选择它们，然后选择 **" 在代理上启用 "** 来启用代理。  
  
3.  在联合服务器代理上更新 IIS 安装，以便将安全断言标记语言 \(SAML\) 和 WS\-信任终结点配置为反映已更新的端口号。 为此，可以使用记事本来修改 web.config 文件中的以下文件，该文件位于联合服务器代理计算机上的 systemdrive%\\inetpub\\adfs\\ls\\ 上。 例如，假设你有一个名为 sts1.contoso.com 的联合服务器，并且新的端口号为444，则在联合服务器代理计算机上浏览到 "记事本" 并打开 web.config 文件，找到以下部分，修改下面突出显示的端口号，然后保存并退出记事本。  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  将联合服务器代理服务用户帐户添加到相关终结点 Url \(ACL\) 的访问控制列表。 例如，如果端口号为1234，并且用于运行 AD FSfederation server 代理服务的用户帐户是网络服务帐户中生成的\-，请在命令提示符下键入以下命令：  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    前面的命令必须在联合服务器和联合服务器代理计算机上运行。  
  
## <a name="additional-references"></a>其他参考  
[清单：设置联合服务器代理](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

