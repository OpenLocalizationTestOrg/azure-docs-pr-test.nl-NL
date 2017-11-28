---
title: aaaConnect tooa VM van Windows Server | Microsoft Docs
description: Meer informatie over hoe tooconnect en aanmelding tooa virtuele machine van Windows hello Azure portal en Hallo Resource Manager-implementatiemodel.
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
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="b777c-103">Hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows</span><span class="sxs-lookup"><span data-stu-id="b777c-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="b777c-104">U Hallo **Connect** knop in hello Azure portal toostart een Remote Desktop (RDP)-sessie op een Windows-bureaublad.</span><span class="sxs-lookup"><span data-stu-id="b777c-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="b777c-105">Eerst maakt u verbinding toohello virtuele machine en u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="b777c-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="b777c-106">Als u tooconnect tooa Windows VM van een Mac probeert, moet u een RDP-client voor Mac, zoals tooinstall [Microsoft Extern bureaublad](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="b777c-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="b777c-107">Verbinding maken met toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b777c-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="b777c-108">Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b777c-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b777c-109">Klik op het menu Hub Hallo **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="b777c-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="b777c-110">Selecteer Hallo virtuele machine uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="b777c-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="b777c-111">Klik op de blade voor de virtuele machine van Hallo Hallo **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b777c-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Schermopname van hello Azure portal weergeeft hoe tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="b777c-113">Als hello **Connect** knop in Hallo portal grijs is en u niet bent verbonden tooAzure via een [Express Route](../../expressroute/expressroute-introduction.md) of [Site-naar-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) verbinding, moet u toocreate en toewijzen van de VM een openbaar IP-adres voordat u extern bureaublad kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b777c-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="b777c-114">Er is meer informatie over [openbare IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b777c-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="b777c-115">Meld u aan toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b777c-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="b777c-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b777c-116">Next steps</span></span>
<span data-ttu-id="b777c-117">Als u ondervindt wanneer u tooconnect probeert, Zie [problemen met extern bureaublad-verbindingen](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b777c-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b777c-118">Dit artikel leidt u door het opsporen en oplossen van veelvoorkomende problemen.</span><span class="sxs-lookup"><span data-stu-id="b777c-118">This article walks you through diagnosing and resolving common problems.</span></span>

