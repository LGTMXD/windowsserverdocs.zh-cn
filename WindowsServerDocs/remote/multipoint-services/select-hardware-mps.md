---
title: 为 MultiPoint Services 系统选择硬件
description: MultiPoint Services 的硬件注意事项
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: e74961a2-bd38-48ae-b1c0-4b3eff761b4a
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 3dca1b68564c977394c1b71f72db0fde5727c861
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859070"
---
# <a name="selecting-hardware-for-your-multipoint-services-system"></a>为 MultiPoint Services 系统选择硬件
生成 MultiPoint 服务系统时，应选择满足 Windows Server 2016 系统要求的计算机。 如果要确定要选择的组件，请考虑以下事项：  
  
-   完整解决方案的目标价格范围。  
  
-   MultiPoint 服务系统可能需要的使用方案的类型，例如，是用户运行的是多媒体程序、使用 word 处理还是生产力计划或浏览 Internet。  
  
-   你的方案是否有大量处理或内存需求。  
  
-   可以同时使用系统的用户数。 如果你计划同时在系统上有多个用户，或者使用系统密集型程序的用户，则应该为系统规划更多的计算能力。  
  
-   工作站的类型。 你需要多少个 USB 端口或视频端口？  
  
-   未来扩展计划。 你是否打算稍后将工作站添加到 MultiPoint 服务系统？ 是否有足够的视频卡插槽、USB 端口或网络分流点？ 你的硬件需要支持多少个额外的用户？  
  
-   物理布局。 有关详细信息，请参阅[MultiPoint Services Site](MultiPoint-services-Site-Planning.md)plan。  
  
MultiPoint 服务系统通常包含以下组件：  
  
-   一台运行 MultiPoint 服务的计算机，其中包括 CPU、RAM、硬盘驱动器和视频卡。  
  
-   每个工作站的监视器、工作站集线器、键盘和鼠标。  
  
-   适用于 MultiPoint 服务工作站的可选外围设备，包括仅供工作站用户使用的扬声器、耳机、麦克风或存储设备。  
  
-   可供 MultiPoint 服务系统的所有用户使用的可选外围设备，直接连接到主机计算机，如打印机、外部硬盘驱动器和 USB 存储设备。  
  
使用以下信息来做出硬件决策：  
  
-   [选择 CPU](#selecting-a-cpu)  
-   [选择硬件组件](#selecting-hardware-components)  
  
## <a name="selecting-a-cpu"></a>选择 CPU  
MultiPoint 服务系统是多\-用户环境，所有用户均连接到一台主计算机。 这会增加 CPU 使用率，因为所有用户共享同一台计算机。 某些任务（如多媒体程序 \(例如，media player 或视频\-编辑软件\)）具有更大的处理需求。 因此，请确保选择可处理对需要支持的用户和类型的用户数量的处理要求的 CPU。  
  
MultiPoint 服务需要基于 x64\-的 CPU，并且必须符合[硬件要求和性能建议](Hardware-Requirements-and-Performance-Recommendations.md)中所述的计算机系统要求。  
  
以下类型的处理器经过测试，可用于具有高\-需求处理程序的 MultiPoint 服务系统，如多媒体程序：  
  
-   **双\-核心处理器：** 最多可支持8个工作站。  
-   **四\-核心处理器：** 最多可支持16个工作站。
-   **具有多线程的四\-核心处理器：** 最多可支持20个工作站。      
-   **六个具有多线程的\-核心处理器：** 最多可支持24个工作站。  
  
使用此信息，选择满足你的 MultiPoint 服务系统处理要求的 CPU。 
> [!NOTE] 
> 如果正在运行视频密集型应用程序，建议每个工作站至少有一个核心。 
  
## <a name="selecting-hardware-components"></a>选择硬件组件  
生成 MultiPoint Services 系统时，请考虑以下可能需要的硬件组件：  
  
-   视频硬件  
  
-   MultiPoint 服务工作站硬件  
  
    -   *USB 集线器*  
  
    -   USB 零客户端  
  
    -   键盘和鼠标设备  
  
    -   监视器  
  
-   外围设备  
  
    -   音频设备，如扬声器和耳机  
  
    -   麦克风  
  
    -   USB 大容量存储设备  
  
选择了 MultiPoint 服务系统的硬件组件后，请确保为组件获取当前 64\-位驱动程序。  
  
以下主题提供详细信息，以帮助你选择 MultiPoint 服务系统的组件：  
  
[选择视频硬件](#selecting-video-hardware)  
[选择 "直接\-视频"\-连接或 USB 零客户端工作站设备](#BKMK_Selectingdirect-video-connectedorUSBzeroclientstationdevices)   
[选择其他工作站外围设备](#selecting-other-station-peripheral-devices)  
[选择 RDP\-通过\-LAN\-连接工作站硬件](#BKMK_SelectingRDP-over-LAN-connectedstationhardware)  
[选择音频设备](#selecting-audio-devices)  
  
## <a name="selecting-video-hardware"></a>选择视频硬件
选择的视频硬件应支持要在 MultiPoint 服务工作站上工作的用户数所需的监视器数量。 此外，不同类型的视频硬件可以为图形\-密集型程序（例如多媒体内容）提供更高级别的\-性能解决方案。  
  
选择可以支持 MultiPoint 服务系统所需的性能类型的监视器的最大数目的视频硬件。 请确保验证你选择的视频硬件的性能，以确保它满足你的性能要求。  
  
> [!NOTE]  
> 必须安装视频驱动程序，该驱动程序支持跨多个监视器扩展桌面。  
  
视频硬件选项包括：  
  
-   使用 PCI 或 PCIe 总线接口的内部视频卡  
  
-   USB 连接的外部视频控制器  
  
以下部分介绍了每种视频硬件类型的功能。 可以组合内部视频卡和外部视频控制器以创建所需的系统。  
  
### <a name="internal-video-cards"></a>内部视频卡  
内置视频卡插入到计算机上的主板上\-。 内部视频卡是一种解决方案，可帮助图形\-密集型多媒体程序的性能。 但是，内部视频卡需要可用 PCI 或 PCIe 插槽，以将\-插到主板。 许多高\-性能视频卡需要一个 PCIe 插槽，但主板上的 PCIe 槽数量有限。 您应该知道您的计算机上提供了哪种视频卡插槽，以便您可以购买正确类型的视频卡。  
  
可以连接到每个视频卡的监视器的数量取决于在卡上使用的 GPU 以及它支持的端口数，这通常介于2到6之间。  
  
选择 "内部视频卡" 时，请选择支持所需监视器数的视频卡，以创建所需数量的直接视频连接工作站。 可支持的监视器的最大数目等于将\-插入到主板中的内部视频卡的数量乘以其中每个视频卡上的监视器端口数。 例如，如果有两个内部视频卡，并且每个卡都有两个监视器端口，则最多可以支持四个监视器。    
  
### <a name="external-video-controllers"></a>外部视频控制器  
USB 零客户端包含外部视频控制器用于将监视器连接到客户端。 USB 零客户端还可能包括耳机、扬声器、麦克风或其他外围设备的连接。  
  
如果你想要在不打开计算机的情况下启用对其他监视器的支持，或者如果你想要支持的工作站比可用的视频输出更多，请选择 USB 零客户端。 例如，如果你先前已将四台监视器插入\-内部视频卡，并且想要另外添加两个监视器，则可以将两个外部视频控制器中的\-插到计算机，并为两个监视器提供空间。 通过这种方式，可以将 USB 零客户端与视频控制器组合在一起，而不是在主板上使用其他 PCI 或 PCIe 槽。  
  
## <a name="selecting-direct-video-connected-or-usb-zero-client-station-devices"></a><a name="BKMK_Selectingdirect-video-connectedorUSBzeroclientstationdevices"></a>选择直接\-视频\-连接或 USB 零客户端工作站设备  
MultiPoint 服务工作站由工作站集线器或 USB 零客户端组成，其中\-中插入了键盘和鼠标，并将\-插入到主计算机或 USB 零客户端的监视器。 其他外围设备可\-接入工作站集线器或 USB 零客户端，但不需要它们来创建 MultiPoint 工作站。 其他外围设备在[选择其他工作站外围设备](#selecting-other-station-peripheral-devices)中进行了介绍。  
  
选择用于创建 MultiPoint 服务工作站的设备应满足使用 MultiPoint 服务的最低要求。 本主题提供了有关以下 MultiPoint 服务工作站设备的要求的详细信息：  
  
-   [选择 USB 集线器](#selecting-usb-hubs)  
-   [选择 USB 零客户端](#selecting-usb-zero-clients)  
-   [选择键盘和鼠标设备](#selecting-keyboards-and-mouse-devices)  
-   [选择监视器](#selecting-monitors)  
  
### <a name="selecting-usb-hubs"></a>选择 USB 集线器  
MultiPoint 服务系统中使用的 USB 集线器可以是通用的 USB 集线器。 此类集线器通常包含四个或更多个 USB 端口，它们允许将多个 USB 设备连接到计算机上的单个 USB 端口。 某些其他设备（如键盘和视频监视器）也可能将 USB 集线器纳入其设计中。  
  
另一个注意事项是使用*外部供电*的集线器，而不是*总线\-支持*的集线器。 通过总线\-接线的集线器，主机提供的当前数量必须足以为插入到中心\-的所有外围设备提供电源，而不会降低系统性能。 使用外部供电的集线器，你可以连接更多外围设备并为所有设备提供充足的电源。 使用外部供电的集线器有助于防止性能问题、端口故障和其他间歇性问题。  
  
为 MultiPoint 服务系统选择 USB 集线器时，请考虑其使用。 集线器可用作*工作站集线器*、*中间集线器*或*下游集线器*。 有关每种中心类型的说明，请参阅下表。 建议所有 USB 设备均为 USB 2.0 或更高版本。
  
||电|  
|-|-----------|  
|工作站集线器|可以是总线\-通电，除非\-的高\-设备接通电源，否则下游集线器将连接到该设备|  
|中间集线器 |应为外部电源|  
|下游中心|可从外部接通电源，或根据插入集线器\-的设备进行总线供电|  
|活动 USB 扩展器电缆|包含 USB 集线器的活动 USB 电缆通常是总线驱动的;因此，不建议将工作站集线器连接到计算机。|  
  
### <a name="selecting-usb-zero-clients"></a>选择 USB 零客户端  
USB 零客户端是包含视频输出的 USB 集线器。 因此，它允许监视器通过 USB 连接连接到计算机。 有关使用 USB 零客户端进行视频的详细信息，请参阅本文档中的[选择视频硬件](#selecting-video-hardware)。 USB 零客户端还可以启用各种 USB 和非\-USB 设备连接到中心。 USB 零客户端由特定硬件制造商生产，它们需要安装\-特定驱动程序的设备。  
  
### <a name="selecting-keyboards-and-mouse-devices"></a>选择键盘和鼠标设备  
将\-插头的键盘和鼠标设备通常为 USB 设备。 某些 USB 零客户端提供 PS\/2 端口，在这种情况下，键盘和鼠标应该使用 PS\/2 连接到工作站集线器。 如果要设置 PS\/2 直接\-视频\-连接工作站，还可以使用 PS\/2 键盘和鼠标。  
  
带有内部集线器的键盘可用作工作站集线器。 但是，所有其他工作站设备都必须使用键盘上的端口连接到内部集线器。 如果此类键盘通过其他集线器连接到计算机，则会将该集线器视为中间集线器。  
  
如果使用的是 "拆分\-屏幕站"，则可能需要考虑使用没有数字板的微型键盘，使这两个键盘可以放置在显示器的前方。  
  
### <a name="selecting-monitors"></a>选择监视器  
应该为每个 MultiPoint 服务工作站提供一个监视器，除非计划\-屏幕。 监视器插入到计算机上的视频卡、USB 零客户端或基于 LAN\-的客户端。 可以使用视频卡、USB 零客户端或基于 LAN\-的客户端支持的任何类型的监视器，包括 CRT 监视器。  
  
某些特殊的监视器包括基于内部 LAN\-的客户端或 USB 零客户端。 此类监视器通常包含音频输入\/输出插孔和用于连接键盘和鼠标的内部 USB 集线器。 它们通过 USB 或 LAN 连接连接到服务器。  
  
#### <a name="display-resolution"></a>显示器分辨率  
工作站显示区域支持的最低分辨率为 512 x 768 像素。 如果 MultiPoint 服务系统启动并发现工作站的显示区域低于最小分辨率，则在该工作站上将显示一个空白屏幕，并且工作站将无法使用。  
  
如果两个电台要将显示监视器共享\-屏幕站，则显示的最低要求为 1024 x 768，因此，生成的单个工作站屏幕区域至少为 512 x 768。 为获得最佳拆分\-屏幕用户体验，建议使用最小分辨率为 1600 x 900 的宽屏幕。  
  
## <a name="selecting-other-station-peripheral-devices"></a>选择其他工作站外围设备  
MultiPoint 服务支持连接到工作站集线器、USB 零客户端或直接连接到计算机的外围设备。 插入工作站集线器的设备将与该特定工作站关联。 将其他设备直接插入到计算机时，可以使用其他设备。 LAN 客户端还可以支持外围设备。  
  
> [!IMPORTANT]  
> 无法将键盘连接到下游集线器 \(例如，插入到工作站集线器中的集线器\)。 如果将键盘插入下游集线器，则插入到下游集线器\-的任何外围设备将不再可用于该工作站。 此行为允许支持菊花\-链式工作站集线器。  
  
**适用于所有工作站**插入计算机的 USB 设备 \(例如，而不是通过工作站集线器\) 可供所有工作站使用。 根据设备，多个用户可以一次使用它，或者一次只有一个用户可以访问它。 下表说明了如何访问 USB 设备。  
  
> [!NOTE]  
> 表中的 "连接到主机" 列是指运行 MultiPoint 服务的计算机与工作站一起在工作站模式下运行时的行为。 如果在控制台模式下运行，则插入到任何位置的外围设备的行为方式与控制台会话中的标准服务器相同。  
  
||已连接到主机|已连接到工作站集线器或下游集线器|  
|-|------------------------------|----------------------------------------------|  
|键盘|不起作用，除非它是 PS/2 工作站的成员。 |可用于单个工作站<p>无法连接到下游集线器|  
|鼠标|不起作用，除非它是 PS/2 工作站的成员。 |可用于单个工作站|  
|扬声器/耳机|不起作用，除非它是 PS/2 工作站的成员。|可用于单个工作站|  
|USB 存储设备|适用于所有工作站|可用于单个工作站|  
|HID 使用者控件|不起作用|可用于单个工作站|  
|其他 USB 设备，如相机、文档读取器和 DVD 驱动器|Windows Server 2012 支持时，适用于所有工作站|Windows Server 2008 R2 支持的所有工作站可用远程桌面服务|  
  
## <a name="selecting-rdp-over-lan-connected-station-hardware"></a><a name="BKMK_SelectingRDP-over-LAN-connectedstationhardware"></a>选择 RDP\-通过\-LAN\-连接工作站硬件  
可以通过使用远程桌面协议连接到远程桌面服务的任何 LAN 客户端都可以成为 MultiPoint 服务工作站。  
  
如果希望 LAN 客户端仅用作 MultiPoint 工作站，则可能需要 "锁定" LAN 客户端。 例如，配置瘦客户端，使其只能连接到 MultiPoint 服务会话，或配置桌面计算机以便删除对桌面图标和 "开始" 菜单项（如 web 浏览器）的访问，以防止直接访问 Internet。 可以使用 LAN 客户端配置工具或组或本地策略进行这些配置。  
  
## <a name="selecting-audio-devices"></a>选择音频设备  
务必要确保在选择音频设备时，可以将其插入到工作站集线器、USB 零客户端或 LAN 客户端。 某些 USB 集线器、USB 零客户端和 LAN 客户端具有模拟音频插孔，可用于传统模拟音频设备 \(例如耳机或 earbuds\)。 没有模拟插孔的工作站集线器可以使用 USB 音频设备。  
  
如果已使用计算机主板上的 PS\/2 个端口配置 PS\/2 直接\-视频\-连接工作站，则必须在计算机的主板上使用模拟音频，以便当 MultiPoint 服务系统在工作站模式下运行时，可以向此工作站提供音频设备。  
  
如果没有 PS\/2 直接\-视频\-连接工作站，系统主板上的主机音频设备将仅在 MultiPoint 服务系统在控制台模式下运行时才可用。  