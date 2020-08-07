---
title: 步骤4安装和配置 RSA and EDGE1
description: 本主题是测试实验室指南的一部分-演示带有 OTP 身份验证的 DirectAccess 和用于 Windows Server 2016 的 RSA SecurID
manager: brianlic
ms.topic: article
ms.assetid: d46ede6f-1a21-414d-b8c3-6b5c87344b9d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1c970a3782286c18f64813c6d1e92ad363870a59
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963983"
---
# <a name="step-4-install-and-configure-rsa-and-edge1"></a>步骤4安装和配置 RSA and EDGE1

>适用于：Windows Server（半年频道）、Windows Server 2016

RSA 是 RADIUS 和 OTP 服务器，在配置 RADIUS 和 OTP 之前安装。

你将执行以下步骤来配置 RSA 部署：

1. 在 RSA 服务器上安装操作系统。 在 RSA 服务器上安装 Windows Server 2016、Windows Server 2012 R2 或 Windows Server 2012。

2. 在 RSA 上配置 TCP/IP。 在 RSA 服务器上配置 TCP/IP 设置。

3. 将身份验证管理器安装文件复制到 RSA 服务器。 在 RSA 上安装操作系统后，将身份验证管理器文件复制到 RSA 计算机。

4. 将 RSA 服务器联接到 CORP 域。 将 RSA 加入 CORP 域。

5. 在 RSA 上禁用 Windows 防火墙。 禁用 RSA 服务器上的 Windows 防火墙。

6. 在 RSA 服务器上安装 RSA 身份验证管理器。 安装 RSA 身份验证管理器。

7. 配置 RSA 身份验证管理器。 配置身份验证管理器。

8. 创建 DAProbeUser。 为探测目的创建用户帐户。

9. 在 CLIENT1 上安装 RSA SecurID 软件令牌。 在 CLIENT1 上安装 RSA SecurID 软件令牌。

10. 将 EDGE1 配置为 RSA 身份验证代理。 在 EDGE1 上配置 RSA Authentication 代理。

11. 配置 EDGE1 以支持 OTP 身份验证。 为 DirectAccess 配置 OTP，并验证配置。

## <a name="install-the-operating-system-on-the-rsa-server"></a><a name="InstallOS"></a>在 RSA server 上安装操作系统

1.  在 RSA 上，开始安装 Windows Server 2016、Windows Server 2012 R2 或 Windows Server 2012。

2.  按照说明完成安装，为本地管理员帐户指定 Windows Server 2016、Windows Server 2012 R2 或 Windows Server 2012 (完全安装) 和强密码。 使用本地管理员账户登录。

3.  将 RSA 连接到具有 Internet 访问权限的网络，然后运行 Windows 更新以安装 Windows Server 2016、Windows Server 2012 R2 或 Windows Server 2012 的最新更新，然后从 Internet 断开连接。

4.  将 RSA 连接到公司网络子网。

## <a name="configure-tcpip-on-rsa"></a><a name="TCP"></a>在 RSA 上配置 TCP/IP

1.  在初始配置任务中，单击 "**配置网络**"。

2.  在 "**网络连接**" 中，右键单击 "**本地连接**"，然后单击 "**属性**"。

3.  单击 **“Internet 协议版本 4 (TCP/IPv4)”**，然后单击 **“属性”**。

4.  单击 **“使用下面的 IP 地址”**。 在“IP 地址”**** 中，键入“10.0.0.5”****。 在 **“子网掩码”** 框中，键入 **255.255.255.0**。 在 "**默认网关**" 中，键入**10.0.0.2**。 单击 "**使用以下 dns 服务器地址**"，在 "**首选 dns 服务器**" 中，键入**10.0.0.1**。

5.  单击 **“高级”**，然后单击 **“DNS”** 选项卡。

6.  在 "**此连接的 DNS 后缀**" 中，键入**corp.contoso.com**，然后单击 **"确定"** 两次。

7.  在 "**本地连接属性**" 对话框中，单击 "**关闭**"。

8.  关闭 **“网络连接”** 窗口。

## <a name="copy-authentication-manager-installation-files-to-the-rsa-server"></a><a name="copyinstfiles"></a>将身份验证管理器安装文件复制到 RSA 服务器

1.  在 RSA 服务器上，创建 C:\RSA 安装的文件夹。

2.  将 RSA Authentication Manager 7.1 SP4 媒体的内容复制到 C:\RSA 安装文件夹中。

3.  创建子文件夹 C:\RSA Installation\License and Token。

4.  将 RSA 许可证文件复制到 C:\RSA Installation\License 和标记。

## <a name="join-the-rsa-server-to-the-corp-domain"></a><a name="JoinDomain"></a>将 RSA 服务器联接到 CORP 域

1.  右键单击**我的电脑**，然后单击 "**属性**"。

2.  在 **“系统属性”** 对话框中的 **“计算机名”** 选项卡上，单击 **“更改”**。

3.  在 "**计算机名**" 中，键入**RSA**。 在 "**成员**" 中，单击 "**域**"，键入**Corp.contoso.com**，然后单击 **"确定"**。

4.  当系统提示你输入用户名和密码时，请键入**User1**和密码，然后单击 **"确定"**。

5.  在 "域对话" 对话框中，单击 **"确定"**。

6.  当系统提示你必须重新启动计算机时，请单击“确定”****。

7.  在“系统属性”**** 对话框中单击“关闭”****。

8.  当系统提示你重新启动计算机时，请单击“立即重新启动”****。

9. 重新启动计算机后，键入**User1**和密码，在 "**登录到：** " 下拉列表中选择 "公司"，然后单击 **"确定"**。

## <a name="disable-windows-firewall-on-rsa"></a><a name="BKMK_Firewall"></a>在 RSA 上禁用 Windows 防火墙

1.  依次单击 "**开始**"、 **"控制面板**"、"**系统和安全**"，然后单击 " **Windows 防火墙**"。

2.  单击 **"打开或关闭 Windows 防火墙"**。

3.  关闭所有设置的**Windows 防火墙**。

4.  单击 **"确定"** 并关闭 Windows 防火墙。

## <a name="install-rsa-authentication-manager-on-the-rsa-server"></a><a name="install"></a>在 RSA server 上安装 RSA 身份验证管理器

1.  如果在此过程中的任何时间出现安全警告消息，请单击 "**运行**" 以继续。

2.  打开 C:\RSA 安装文件夹，然后双击**autorun.exe**"。

3.  单击 "**立即安装**"，单击 "**下一步**"，选择美洲的顶层选项，然后单击 "**下一步**"。

4.  选择 **"我接受许可协议的条款**"，然后单击 "**下一步**"。

5.  选择 "**主实例**"，然后单击 "**下一步**"。

6.  在 "**目录名称：** " 字段中键入**C:\RSA**，然后单击 "**下一步**"。

7.  验证服务器名称 (RSA.corp.contoso.com) 和 IP 地址是否正确，然后单击 "**下一步**"。

8.  浏览到 C:\RSA Installation\License and Token，并单击 "**下一步**"。

9. 在 "**验证许可证文件**" 页上，单击 "**下一步**"。

10. 在 "**用户 ID** " 字段中，键入 "**管理员**"，然后在 "**密码**" 和 "**确认密码**" 字段中键入强密码。 单击“下一步”。

11. 在 "日志选择" 屏幕上，接受默认值，然后单击 "**下一步**"。

12. 在 "摘要" 屏幕上，单击 "**安装**"。

13. 安装完成后，单击 "**完成**"。

## <a name="configure-rsa-authentication-manager"></a><a name="confiauthmgr"></a>配置 RSA 身份验证管理器

1.  如果 RSA 安全控制台未自动打开，则在 RSA 计算机桌面上双击 "RSA Security Console"。

2.  如果出现 "安全证书警告/安全警报"，请单击 "**继续浏览此网站**" 或单击 **"是"** 以继续操作，并将此站点添加到受信任的站点（如果请求）。

3.  在 "**用户 ID** " 字段中，键入**管理员**，然后单击 **"确定"**。

4.  在 "**密码**" 字段中，键入管理员帐户的密码，并单击 "**登录**"。

5.  插入令牌信息。

    1.  在**RSA Security Console**中，单击 "**身份验证**"，然后单击 " **SecurID 令牌**"。

    2.  单击 "**导入令牌作业**"，然后单击 "**新建**"。

    3.  在 "**导入选项**" 部分，单击 "**浏览**"。 浏览到并选择 C：\ 中的标记 XML 文件RSA Installation\License 和 Token 文件夹，然后单击 "**打开**"。

    4.  单击页面底部的 "**提交作业**"。

6.  创建 OTP 新用户。

    1.  在**RSA Security Console**中，单击 **"标识**" 选项卡，单击 "**用户**"，然后单击 "**添加新**项"。

    2.  在 "**姓氏：** 节类型" "**用户**" 中，在 "**用户 ID：** " 部分键入**User1** (USERID 必须与用于此实验室) 的 AD 用户名相同。  在 "**密码：** " 和 "**确认密码：** " 部分键入强密码。 清除 **"要求用户在下次登录时更改密码"** 复选框，并单击 "**保存**"。

7.  将 User1 分配到导入的一个令牌。

    1.  在 "**用户**" 页上，单击**User1** ，然后单击 " **SecurID 标记**"。

    2.  单击 " **SecurID 令牌**"，然后单击 "**分配令牌**"。

    3.  在**序列号**标题下，单击列出的第一个数字，然后单击 "**分配**"。

    4.  单击已分配的令牌，然后单击 "**编辑**"。 在 " **SECURID Pin 管理**" 部分中的 "**用户身份验证要求**" 中，选择 "**不要求 PIN (仅限令牌) **。

    5.  单击 "**保存并分发令牌**"。

    6.  在 "**基本**信息" 部分的 "**分发软件令牌**" 页上，单击 "**颁发令牌文件 (SDTID) **"。

    7.  在 "**令牌文件选项**" 部分的 "**分发软件令牌**" 页上，清除 "**启用复制保护**" 复选框。 单击 "**无密码**" 和 "**下一步**"。

    8.  在 "**下载文件**" 部分的 "**分发软件令牌**" 页上，单击 "**立即下载**"。 单击“保存”  。 浏览到 C:\RSA 安装，并单击 "**保存**并**关闭**"。

    9. 最大程度地减少**RSA Security Console** ，以备日后使用。

8.  将身份验证管理器配置为 RADIUS 服务器。

    1.  在 RSA 计算机桌面上，双击 **"Rsa 安全操作控制台"**。

    2.  如果出现 "安全证书警告/安全警报"，请单击 "**继续浏览此网站**" 或单击 **"是"** 以继续操作，并将此站点添加到受信任的站点（如果请求）。

    3.  输入用户 ID 和密码，并单击 "**登录"**。

    4.  单击 "**部署配置-RADIUS-配置服务器**"。

    5.  在 "**需要其他凭据**" 页上，输入管理员用户 ID 和密码，然后单击 **"确定"**。

    6.  在 "**配置 RADIUS 服务器**" 页**上，输入**用于管理员用户的密码和**主密码**的相同密码。 输入管理员用户 ID 和密码，然后单击 "**配置**"。

    7.  验证是否显示 **"已成功配置 RADIUS 服务器"** 消息。 单击“Done”（完成） 。 关闭**RSA 操作控制台**。

    8.  切换回 **"RSA Security Console"**。

    9. 在 " **radius** " 选项卡上，单击 " **radius 服务器**"。 验证是否列出了 rsa.corp.contoso.com。

9. 将 RSA server 配置为 RSA Authentication 客户端。

    1.  在 " **radius** " 选项卡上，单击 " **radius 客户端**" 并**添加新**。

    2.  单击 "**任何 RADIUS 客户端**" 复选框。

    3.  在 "**共享机密**" 字段中键入所选的强密码。 稍后，将 EDGE1 配置为 OTP 时，将使用此相同的密码。

    4.  将 " **IP 地址**" 字段留空，并将 "**品牌/型号**" 项保留为**标准半径**。

    5.  单击 "**保存但不包含 RSA 代理**"。

10. 创建将 EDGE1 配置为 RSA 身份验证代理所需的文件。

    1.  在 "**访问**" 选项卡上，突出显示 "**身份验证代理**"，然后单击 "**新建**"。

    2.  在 "**主机名**" 字段中键入**EDGE1** ，并单击 "**解析 IP**"。

    3.  请注意，EDGE1 的 IP 地址现在显示在 " **Ip 地址**" 字段中。 单击“保存”  。

11.  ( # A0) 为 EDGE1 服务器生成配置文件。

    1.  在 "**访问**" 选项卡上，突出显示 "**身份验证代理**" 并单击 "**生成配置文件**"。

    2.  在 "**生成配置文件**" 页上，单击 "**生成配置文件**"，然后单击 "**立即下载**"。

    3.  单击 "**保存**"，浏览到 C：\RSA 安装，然后单击 "**保存**"。

    4.  单击 "**下载完成**" 对话框上的 "**关闭**"。

12.  ( # A0) 为 EDGE1 服务器生成节点机密文件。

    1.  在 "**访问**" 选项卡上，突出显示 "**身份验证代理**" 并单击 "**管理现有**"。

    2.  单击当前配置的节点 EDGE1，并单击 "**管理节点机密**"。

    3.  选中 "**创建新的随机节点密码"，然后选中 "将节点机密导出到文件**" 复选框。

    4.  在 "**加密密码**" 和 "**确认加密密码**" 字段中输入用于管理员用户的相同密码，然后单击 "**保存**"。

    5.  在 "**节点密钥文件生成**" 页上，单击 "**立即下载**"。

    6.  在 "**文件下载**" 对话框中，单击 "**保存**"，浏览到 C:\RSA 安装，并单击 "**保存**"。 单击 "**下载完成**" 对话框上的 "**关闭**"。

    7.  从 RSA Authentication Manager 媒体副本 \auth_mgr\windows-x86_64\am\rsa-ace_nsload\win32-5.0-x86\agent_nsload.exe 到 C:\RSA 安装。

## <a name="create-daprobeuser"></a><a name="BKMK_DAProbeUser"></a>创建 DAProbeUser

1.  在**RSA Security Console**中，单击 **"标识**" 选项卡，单击 "**用户**"，然后单击 "**添加新**项"。

2.  在 "**姓氏：** 节类型"**探测器**中，在 "**用户 ID：** " 节中键入**DAProbeUser**。 在 "**密码：** " 和 "**确认密码：** " 部分键入强密码。 清除 **"要求用户在下次登录时更改密码"** 复选框，并单击 "**保存**"。

## <a name="install-rsa-securid-software-token-on-client1"></a><a name="InstToken"></a>在 CLIENT1 上安装 RSA SecurID 软件令牌
使用此过程在 CLIENT1 上安装 SecurID 软件令牌。

#### <a name="install-securid-software-token"></a>安装 SecurID 软件令牌

1.  在 CLIENT1 计算机上创建文件夹 C:\RSA Files。 将 Software_Tokens.zip 从 RSA 计算机上的 C:\RSA 安装中的文件复制到 C:\RSA 文件。 将 SDTID User1_000031701832 文件提取到 CLIENT1 上的 C:\RSA 文件中。

2.  访问 RSA SecurID 软件令牌媒体源，并在**SecurID SoftwareToken 客户端应用**文件夹中双击 "RSASECURIDTOKEN410" 以启动 RSA SecurID 安装。 如果显示 "**打开文件-安全警告**" 消息，则单击 "**运行**"。

3.  在**RSA SecurID Software InstallShield 向导**对话框上，单击 "**下一步**" 两次。

4.  接受许可协议，然后单击 "**下一步**"。

5.  在 "**安装类型**" 对话框**中，依次选择 "****下一步**" 和 "**安装**"。

6.  如果出现了“用户帐户控制”**** 对话框，请确认其所显示的操作是你要采取的操作，然后单击“是”****。

7.  选中 "**启动 RSA SecurID 软件令牌**" 复选框，然后单击 "**完成**"。

8.  单击 "**从文件导入**"。

9. 单击 "**浏览**"，选择 "C:\RSA Files \ USER1_000031701832. SDTID"，然后单击 "**打开**"。

10. 单击“确定”两次****。

## <a name="configure-edge1-as-an-rsa-authentication-agent"></a><a name="configAuthAgt"></a>将 EDGE1 配置为 RSA 身份验证代理
使用此过程配置 EDGE1 以执行 RSA 身份验证。

#### <a name="configure-the-rsa-authentication-agent"></a>配置 RSA 身份验证代理

1. 在 EDGE1 上打开 Windows 资源管理器并创建文件夹 C:\RSA Files。 浏览到 RSA ACE 安装介质。

2. 将文件 agent_nsload.exe、AM_Config.zip 和 EDGE1_NodeSecret.zip 从 RSA media 复制到 C:\RSA 文件。

3. 将两个 zip 文件的内容提取到以下位置：

   1.  C：\Windows\system32

   2.  C：\Windows\SysWOW64

4. 将 agent_nsload.exe 复制到 C:\Windows\SysWOW64 \\ 。

5. 打开提升的命令提示符并导航到 C:\windows\syswow64。

6. 键入**agent_nsload.exe-f nodesecret-p <password> ** ，其中是在 <password> 初始 RSA 配置过程中创建的强密码。 按 Enter。

7. 将 C:\Windows\SysWOW64\securid 复制到 C:\Windows\System32。

## <a name="configure-edge1-to-support-otp-authentication"></a><a name="configOTP"></a>配置 EDGE1 以支持 OTP 身份验证
使用此过程为 DirectAccess 配置 OTP，并验证配置。

#### <a name="configure-otp-for-directaccess"></a>为 DirectAccess 配置 OTP

1.  在 EDGE1 上，打开服务器管理器，然后在左窗格中单击 "**远程访问**"。

2.  右键单击 "服务器" 窗格中的 " **EDGE1** "，然后选择 "**远程访问管理**"。

3.  单击“配置”。

4.  在 " **DirectAccess 设置**" 窗口中的 "**步骤 2-远程访问服务器**" 下，单击 "**编辑**"。

5.  单击 "**下一步**" 三次，然后在 "**身份验证**" 部分中选择 "双重**身份验证**" 和 "**使用 OTP**"，并确保选中 "**使用计算机证书**"。 验证根 CA 是否设置为**CN = APP1-ca**。 单击“下一步”。

6.  在 " **OTP RADIUS 服务器**" 部分中，双击 "空白**服务器名称**" 字段。

7.  在 "**添加 RADIUS 服务器**" 对话框中，在 "**服务器名称**" 字段中键入**RSA** 。 单击 "**共享机密**" 字段旁边的 "**更改**"，然后键入在**新**密码中的 RSA 服务器上配置 RADIUS 客户端时使用的相同密码，并**确认新的机密**字段。 单击 **"确定"** 两次，然后单击 "**下一步**"。

    > [!NOTE]
    > 如果 RADIUS 服务器所在的域不同于远程访问服务器，则 "**服务器名称**" 字段必须指定 RADIUS 服务器的 FQDN。

8.  在 " **OTP CA 服务器**" 部分中，选择 "APP1.corp.contoso.com"，然后单击 "**添加**"。 单击“下一步”。

9. 在 " **OTP 证书模板**" 页上，单击 "**浏览**" 选择用于注册用于 OTP 身份验证的证书的证书模板，然后在 "**证书模板**" 对话框中选择 " **DAOTPLogon**"。 单击“确定”。 单击 "**浏览**" 选择用于注册远程访问服务器用于签署 OTP 证书注册请求的证书的证书模板，然后在 "**证书模板**" 对话框中选择 " **DAOTPRA**"。 单击“确定”  。 单击“下一步”。 

10. 在 "**远程访问服务器设置**" 页上，单击 "**完成**"，然后单击 " **DirectAccess 专家向导**" 上的 "**完成**"。

11. 在 "**远程访问查看**" 对话框中，单击 "**应用**"，等待 DirectAccess 策略更新，然后单击 "**关闭**"。

12. 在 "**开始**" 屏幕上，键入 "**powershell.exe**"，右键单击 " **Powershell**"，单击 "**高级**"，然后单击 "以**管理员身份运行**"。 如果出现了“用户帐户控制”**** 对话框，请确认其所显示的操作是你要采取的操作，然后单击“是”****。

13. 在 Windows PowerShell 窗口中，键入**gpupdate/force** ，然后按 enter。

14. 关闭并重新打开远程访问管理控制台，并验证所有 OTP 设置是否正确。



