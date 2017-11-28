---
title: aaaAbout ExpressRoute virtuele netwerkgateways | Microsoft Docs
description: Meer informatie over virtuele netwerkgateways voor ExpressRoute.
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="122e7-103">Virtuele netwerkgateways voor ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="122e7-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="122e7-104">Een virtuele netwerkgateway wordt gebruikt toosend netwerkverkeer tussen virtuele netwerken van Azure en lokale locaties.</span><span class="sxs-lookup"><span data-stu-id="122e7-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="122e7-105">Wanneer u een ExpressRoute-verbinding configureert, moet u maken en configureren van een virtuele netwerkgateway en een verbinding met virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="122e7-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="122e7-106">Wanneer u een gateway voor een virtueel netwerk maakt, geeft u verschillende instellingen op.</span><span class="sxs-lookup"><span data-stu-id="122e7-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="122e7-107">Een van de instellingen Hallo vereist geeft aan of Hallo gateway wordt gebruikt voor ExpressRoute of Site-naar-Site VPN-verkeer.</span><span class="sxs-lookup"><span data-stu-id="122e7-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="122e7-108">Hallo Resource Manager-implementatiemodel, Hallo-instelling is '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="122e7-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="122e7-109">Wanneer netwerkverkeer op een persoonlijke verbinding die wordt verzonden, gebruikt u het Gatewaytype Hallo 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="122e7-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="122e7-110">Dit is ook bedoeld tooas een ExpressRoute-gateway.</span><span class="sxs-lookup"><span data-stu-id="122e7-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="122e7-111">Wanneer netwerkverkeer verzonden versleutelde via openbaar Internet hello, gebruikt u Gatewaytype Hallo 'VPN-'.</span><span class="sxs-lookup"><span data-stu-id="122e7-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="122e7-112">Dit is bedoeld tooas een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="122e7-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="122e7-113">Site-naar-site-, punt-naar-site- en VNet-naar-VNet-verbindingen gebruiken allemaal een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="122e7-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="122e7-114">Elk virtueel netwerk kan maar één virtuele netwerkgateway per type gateway hebben.</span><span class="sxs-lookup"><span data-stu-id="122e7-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="122e7-115">U kunt voor een virtueel netwerk bijvoorbeeld één gateway gebruiken die -GatewayType Vpn gebruikt en één die -GatewayType ExpressRoute gebruikt.</span><span class="sxs-lookup"><span data-stu-id="122e7-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="122e7-116">Dit artikel is gericht op Hallo ExpressRoute virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="122e7-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="122e7-117"><a name="gwsku"></a>Gateway-SKU's</span><span class="sxs-lookup"><span data-stu-id="122e7-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="122e7-118">Als u wilt dat tooupgrade uw gateway tooa krachtiger Hallo gateway-SKU, in de meeste gevallen kunt u 'Formaat AzureRmVirtualNetworkGateway' PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="122e7-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="122e7-119">Dit werkt voor upgrades tooStandard en HighPerformance SKU's.</span><span class="sxs-lookup"><span data-stu-id="122e7-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="122e7-120">Tooupgrade toohello UltraPerformance SKU, u moet echter toorecreate Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="122e7-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="122e7-121"><a name="aggthroughput"></a>Geschatte geaggregeerde doorvoer per gateway-SKU</span><span class="sxs-lookup"><span data-stu-id="122e7-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="122e7-122">Hallo volgende tabel toont Hallo gatewaytypen en Hallo geschatte geaggregeerde doorvoer.</span><span class="sxs-lookup"><span data-stu-id="122e7-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="122e7-123">Deze tabel is van toepassing tooboth Hallo Resource Manager en de klassieke implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="122e7-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="122e7-124">Doorvoer van de toepassing afhankelijk is van meerdere factoren, zoals Hallo end-to-end-latentie, en het Hallo-nummer van het verkeer stroomt Hallo toepassing wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="122e7-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="122e7-125">Hallo getallen in Hallo tabel vertegenwoordigen Hallo bovengrens theorectically, kunt u de toepassing hello bereiken in een omgeving met ideaal.</span><span class="sxs-lookup"><span data-stu-id="122e7-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="122e7-126"><a name="resources"></a>REST-API's en PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="122e7-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="122e7-127">Zie voor aanvullende technische bronnen en specifieke syntaxis vereisten bij het gebruik van REST-API's en PowerShell-cmdlets voor gateway-configuraties van virtuele netwerken, Hallo pagina's te volgen:</span><span class="sxs-lookup"><span data-stu-id="122e7-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="122e7-128">**Klassiek**</span><span class="sxs-lookup"><span data-stu-id="122e7-128">**Classic**</span></span> | <span data-ttu-id="122e7-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="122e7-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="122e7-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="122e7-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="122e7-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="122e7-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="122e7-132">REST API</span><span class="sxs-lookup"><span data-stu-id="122e7-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="122e7-133">REST API</span><span class="sxs-lookup"><span data-stu-id="122e7-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="122e7-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="122e7-134">Next steps</span></span>
<span data-ttu-id="122e7-135">Zie [overzicht van ExpressRoute](expressroute-introduction.md) voor meer informatie over beschikbare verbinding configuraties.</span><span class="sxs-lookup"><span data-stu-id="122e7-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

