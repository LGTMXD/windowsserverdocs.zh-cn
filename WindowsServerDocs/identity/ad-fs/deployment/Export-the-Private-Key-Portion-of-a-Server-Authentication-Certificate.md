---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: 导出服务器身份验证证书的私钥部分
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6baa734e3fc346d94f4387e2ed54d3e707e5af75
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855420"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>导出服务器身份验证证书的私钥部分

Active Directory 联合身份验证服务 \(AD FS\) 场中的每个联合服务器都必须有权访问服务器身份验证证书的私钥。 如果要实现联合服务器或 Web 服务器的服务器场，则必须具有单个身份验证证书。 此证书必须由 \(CA\)的企业证书颁发机构颁发，并且该证书必须具有可导出的私钥。 服务器身份验证证书的私钥必须可导出，以便使其可用于该服务器场中的所有服务器。  
  
对于服务器场中的所有联合服务器代理必须共享相同服务器身份验证证书的私钥部分，这是联合服务器代理场的相同概念。  
  
> [!NOTE]  
> 中的 AD FS 管理 "管理单元\-是指作为服务通信证书的联合服务器的服务器身份验证证书。  
  
根据此计算机将扮演的角色，在使用私钥安装了服务器身份验证证书的联合服务器计算机或联合服务器代理计算机上使用此过程。 当完成该过程时，就可以在服务器场中的每个服务器的默认网站上导入此证书。 有关详细信息，请参阅将[服务器身份验证证书导入到默认](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)网站。  
  
若要完成此过程，至少需要是本地计算机上的**管理员**组或等效组中的成员。  可在[本地默认组和域默认组](https://go.microsoft.com/fwlink/?LinkId=83477)中查看有关使用适合的帐户和组成员身份的详细信息。   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>导出服务器身份验证证书的私钥部分  
  
1. 在 "**开始**" 屏幕上，键入 "**Internet Information Services \(IIS\) 管理器**"，然后按 enter。  
  
2. 在控制台树中单击 **“ComputerName”** 。  
  
3. 在中心窗格中，双击 "**服务器证书**"\-"。  
  
4. 在中心窗格中，右键\-单击要导出的证书，然后单击 "**导出**"。  
  
5. 在 "**导出证书**" 对话框中，单击 " **...** " 按钮。  
  
6. 在 **"文件名"** 中，键入**C：\\** <em>NameofCertificate</em>，然后单击 "**打开**"。  
  
7. 键入证书的密码、进行确认，然后单击“确定”。  
  
8. 通过确认指定的文件创建在指定的位置上来验证导出成功。  
  
   > [!IMPORTANT]  
   > 必须将该文件传输到物理媒体，并在传输到新服务器的过程中保护其安全，以便可以将此证书导入到新服务器上的本地证书存储中。 保护私钥的安全非常重要。 如果此密钥泄露，则整个 AD FS 部署的安全性 \(包含组织内和资源伙伴组织中的资源\) 受到威胁。  
  
9. 请在安装联合身份验证服务之前，将已导出的服务器身份验证证书导入到新的服务器上的证书存储区。 有关如何导入证书的信息，请参阅导入服务器证书 \([http：\/\/go.microsoft.com\/fwlink\/？LinkId\=108283](https://go.microsoft.com/fwlink/?LinkId=108283)\)。  
  
## <a name="additional-references"></a>其他参考  
[清单：设置联合服务器](Checklist--Setting-Up-a-Federation-Server.md)  
  
[清单：设置联合服务器代理](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[联合服务器的证书要求](https://technet.microsoft.com/library/dd807040.aspx)  
  
[联合服务器代理的证书要求](https://technet.microsoft.com/library/dd807054.aspx)  
  

