---
redirect_url: /windows-server/windows-server
ms.openlocfilehash: 9ef5565af748b4dd592e71ec4bd34a2be58003d9
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "75947297"
---
# <a name="windows-server-2016"></a>Windows Server 2016

此库为 IT 专业人员提供评估、规划、部署、保护和管理 Windows Server 2016 的信息。

> [!Note] 
> 下一版本的 Windows Server 有所更改！ 若要查找有关新增功能的详细信息，请访问 [Windows Server 半年频道概述](./get-started/semi-annual-channel-overview.md)。 

[![Windows Server 2016 概述视频](media/front-page-video.png)](https://www.youtube-nocookie.com/embed/V8oF0JpDzaM)

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/what-s-new-in-windows-server-2016"> &lt;img height=145 src=&quot;media/whats-new-highlight.png&quot; alt=&quot;“新增功能”图标&quot; title=&quot;Windows Server 16 中有什么新增功能？&quot;/&gt;</a>
        <br/>新增功能
    </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/server-basics"> &lt;img height=145 src=&quot;media/1-getstarted.png&quot; alt=&quot;“开始使用”图标&quot; title=&quot;开始使用 Windows Server 16&quot; /&gt;</a>
      <br/>入门 </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/administration/index"> &lt;img height=145 src=&quot;media/8-management.png&quot; alt=&quot;“管理”图标&quot; title=&quot;管理 Windows Server&quot; /&gt;</a>
      <br/>管理 </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/failover-clustering/failover-clustering-overview"> &lt;img height=145 src=&quot;media/3-failover.png&quot; alt=&quot;“故障转移群集”图标&quot; title=&quot;Windows Server 故障转移群集&quot; /&gt;</a>
      <br/>故障转移群集 </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/identity/identity-and-access"> &lt;img height=145 src=&quot;media/4-identity.png&quot; alt=&quot;“身份标识和访问控制”图标&quot; title=&quot;Windows Server 身份标识和访问控制&quot; /&gt;</a>
      <br>身份标识和访问控制 </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/networking/networking"> &lt;img height=145 src=&quot;media/6-networking.png&quot; alt=&quot;“网络”图标&quot; title=&quot;Windows Server 网络&quot; /&gt; </a>
      <br/>网络 </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/remote/index"> &lt;img height=145 src=&quot;media/remote.png&quot; alt=&quot;“远程”图标&quot; title=&quot;远程访问和服务器管理&quot; /&gt; </a>
      <br/>远程访问 </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/security/security-and-assurance"> &lt;img height=145 src=&quot;media/5-security.png&quot; alt=&quot;“安全”图标&quot; title=&quot;Windows Server 安全和保障&quot; /&gt; </a>
      <br/>安全和保障 </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">&nbsp;</td>
    <td align='center' style="width:25%; border:0;"><br>
      <a href="/windows-server/storage/storage"> &lt;img height=145 src=&quot;media/7-storage.png&quot; alt=&quot;“存储”图标&quot; title=&quot;Windows Server 存储&quot; /&gt; </a>
      <br/>存储 </td>
   <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/virtualization/virtualization"> &lt;img height=145 src=&quot;media/virtualization.png&quot; alt=&quot;“虚拟化”图标&quot; title=&quot;Windows Server 虚拟化&quot; /&gt;</a>
      <br/>虚拟化 </td>
    <td align='center' style="width:25%; border:0;">[https://blogs.technet.microsoft.com/askperf/2008/11/18/disabling-unnecessary-services-a-word-to-the-wise/](&nbsp;) </td>
  </tr>
</table>

<br/>

> [!Note] 
> 若要体验 Windows Server 2016 中的第一手新功能和特性，可以访问 [Windows Server 评估](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)下载评估版本。 


## <a name="windows-server-2016-editions"></a>Windows Server 2016 版本

Windows Server 2016 有 Standard、Datacenter 和 Essentials 版本。 Windows Server 2016 Datacenter 包括无限虚拟化权限，以及构建软件定义数据中心的新功能。 Windows Server 2016 Standard 提供企业级功能，具有有限的虚拟化权限。 Windows Server Essentials 是连接云的首选服务器。 它有自己的[内容详实的文档](https://go.microsoft.com/fwlink/?LinkID=827171)，此处的内容侧重于 Standard 和 Datacenter 版本。 下表简要概括了 Standard 和 Datacenter 版本的主要差异：

|功能|数据中心版|Standard|  
|-------------------|----------|-----------------------|  
|Windows Server 的核心功能| 是| 是|
|OSE / Hyper-V 容器|无限制|   2|
|Windows Server 容器|无限制|   无限制|
|主机保护者服务| 是| 是|
|Nano Server 安装选项| 是| 是|
|存储功能包括存储空间直通和存储副本| 是| 否|
|受防护的虚拟机| 是| 否|
|软件定义的网络基础结构（网络控制器、软件负载均衡器和多租户网关）| 是| 否|

有关详细信息，请参阅 [Pricing and licensing for Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server-pricing)（Windows Server 2016 的定价和许可）和 [Compare features in Windows Server versions](https://www.microsoft.com/cloud-platform/windows-server-comparison)（比较 Windows Server 版本中的功能）。

## <a name="installation-options"></a>安装选项

Standard 和 Datacenter 版本都提供了三种安装选项：

- **服务器核心：** 减少了磁盘上所需的空间、潜在的攻击面，尤其减少了维护要求。 **推荐**使用此选项，除非对其他用户界面元素和图形管理工具有特殊要求。
- **带有桌面体验的服务器：** 安装标准用户界面和所有工具，其中包括需要在 Windows Server 2012 R2 中单独安装的客户端体验功能。 将会通过服务器管理器或其他方法安装服务器角色和功能。
- **Nano Server：** 是远程管理的服务器操作系统，已专门针对私有云和数据中心进行了优化。 类似于 Windows Server 的“服务器核心”模式，但显著变小了，无本地登录功能，且仅支持 64 位应用程序、工具和代理。 其所需的磁盘空间更小，启动速度明显更快，且所需的更新和重启操作远远少于其他选项。

>[!Note]
> 与某些之前版本的 Windows Server 不同，安装后无法在服务器核心和具有桌面体验的服务器之间转换。 例如，如果安装服务器核心，但后来决定使用具有桌面体验的服务器，则应重新安装（反之亦然）。


知道哪个版本和安装选项最适合自己后，单击下方开始使用 Windows Server 2016。
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:33%; border:0;">
      <a  href="/windows-server/get-started/getting-started-with-nano-server"> <img width="175" src="media/nano.png" alt="Icon representing Nano server" title="Nano Server - 轻量级" /><br/>Nano Server - <br/>轻量级</a>
    </td>
    <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-core"> <img width="175" src="media/servercore.png" alt="Icon representing the Server Core installation" title="服务器核心 - 建议" /><br/>服务器核心 - <br/>建议</a></td>
   <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-with-desktop-experience"><img width="175" src="media/desktop.png" alt="Icon representing the full desktop experience installation option for Windows Server" title="桌面体验 - 完整体验" /><br/>桌面体验 - <br/>完整界面</a></td>
  </tr>
</table>

## <a name="windows-server-software-defined-datacenter-sddc"></a>Windows Server 软件定义数据中心 (SDDC)

虚拟化存储、网络、安全和管理技术是 Windows Server 软件定义数据中心 (SDDC) 的构建基块。
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:10%; border:0;"></td>
    <td align='center' style="width:50%; border:0;"><a href="/windows-server/sddc"><img width="400" src="media/sddc/WS16-heading.png" alt="Icon representing SDDC" title="Windows Server 软件定义数据中心 (SDDC)" /><br/>Windows Server 软件定义数据中心 (SDDC)</a></td>
    <td align='center' style="width:10%; border:0;"></td>
  </tr>
</table>
