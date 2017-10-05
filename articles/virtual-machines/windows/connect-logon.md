---
title: Verbinding maken met een virtuele Windows Server-machine | Microsoft Docs
description: Leer hoe u verbinding maakt en u aanmeldt bij een virtuele Windows-machine via de Azure-portal en het Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: 88431377a36d5bc36220c630f0c8d4a46ab4a434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="256fc-103">Verbinding maken met en aanmelden bij een virtuele machine in Azure waarop Windows wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="256fc-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="256fc-104">U gebruikt de knop **Verbinden** in Azure Portal om een Extern bureaublad-sessie (RDP) te starten vanaf een Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="256fc-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="256fc-105">Eerst maakt u verbinding met de virtuele machine en vervolgens meldt u zich aan.</span><span class="sxs-lookup"><span data-stu-id="256fc-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="256fc-106">Als u vanaf een Mac probeert verbinding te maken met een virtuele Windows-machine, moet u een RDP-client voor Mac installeren, zoals [Microsoft Extern bureaublad](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="256fc-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="256fc-107">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="256fc-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="256fc-108">Meld u aan bij de [Azure-portal](https://portal.azure.com/) als u dat nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="256fc-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="256fc-109">Klik in het menu Hub op **Virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="256fc-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="256fc-110">Selecteer de virtuele machine in de lijst.</span><span class="sxs-lookup"><span data-stu-id="256fc-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="256fc-111">Klik op de blade voor de virtuele machine op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="256fc-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![Schermafbeelding van de Azure-portal waarin wordt getoond hoe u verbinding maakt met uw virtuele machine.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="256fc-113">Als de knop **Verbinden** in de portal grijs is en u niet met Azure bent verbonden via een [Snelle route](../../expressroute/expressroute-introduction.md) of een [VPN-tussen-sites](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)-verbinding, moet u een openbaar IP-adres maken en toewijzen aan uw virtuele machine voordat u Extern bureaublad kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="256fc-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="256fc-114">Er is meer informatie over [openbare IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="256fc-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="256fc-115">Aanmelden bij de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="256fc-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="256fc-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="256fc-116">Next steps</span></span>
<span data-ttu-id="256fc-117">Zie [Problemen oplossen met Extern bureaublad-verbindingen](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) als u problemen hebt wanneer u verbinding probeert te maken.</span><span class="sxs-lookup"><span data-stu-id="256fc-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="256fc-118">Dit artikel leidt u door het opsporen en oplossen van veelvoorkomende problemen.</span><span class="sxs-lookup"><span data-stu-id="256fc-118">This article walks you through diagnosing and resolving common problems.</span></span>

