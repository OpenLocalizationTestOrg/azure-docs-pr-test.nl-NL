---
title: aaaLegacy virtuele Azure-netwerkgateway-SKU's | Microsoft Docs
description: Oude virtual network gateway-SKU's.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="f0208-103">Werken met virtuele netwerkgateway SKU's (verouderde SKU's)</span><span class="sxs-lookup"><span data-stu-id="f0208-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="f0208-104">In dit artikel bevat informatie over Hallo oudere (oude) virtuele netwerkgateway SKU's.</span><span class="sxs-lookup"><span data-stu-id="f0208-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="f0208-105">Hallo legacy SKU's werkt nog steeds in beide implementatiemodellen voor VPN-gateways die al zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0208-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="f0208-106">Klassieke VPN-gateways gaan toouse Hallo verouderde SKU's, zowel voor gateways voor bestaande en nieuwe gateways.</span><span class="sxs-lookup"><span data-stu-id="f0208-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="f0208-107">Bij het maken van nieuwe Resource Manager VPN gateways, gebruik Hallo nieuwe gateway-SKU's.</span><span class="sxs-lookup"><span data-stu-id="f0208-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="f0208-108">Zie voor informatie over Hallo nieuwe SKU's, [over VPN-Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="f0208-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="f0208-109"><a name="gwsku"></a>Gateway-SKU's</span><span class="sxs-lookup"><span data-stu-id="f0208-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="f0208-110"><a name="agg"></a>Geschatte geaggregeerde doorvoer per SKU</span><span class="sxs-lookup"><span data-stu-id="f0208-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="f0208-111"><a name="config"></a>Ondersteunde configuraties op SKU- en VPN-type</span><span class="sxs-lookup"><span data-stu-id="f0208-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="f0208-112"><a name="resize"></a>Een gateway (wijziging een gateway-SKU) vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="f0208-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="f0208-113">U kunt het formaat van een gateway-SKU binnen Hallo dezelfde SKU-serie.</span><span class="sxs-lookup"><span data-stu-id="f0208-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="f0208-114">Als u een standaard SKU hebt, kunt u bijvoorbeeld tooa HighPerformance SKU grootte.</span><span class="sxs-lookup"><span data-stu-id="f0208-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="f0208-115">U kunt geen grootte van uw VPN-gateways tussen Hallo oude SKU's en nieuwe SKU families Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0208-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="f0208-116">U kunt niet bijvoorbeeld gaan van een standaard SKU tooa VpnGw2 SKU.</span><span class="sxs-lookup"><span data-stu-id="f0208-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="f0208-117">tooresize een gateway-SKU voor Hallo klassieke implementatiemodel, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f0208-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="f0208-118">tooresize gateway SKU voor Resource Manager-implementatiemodel, Hallo Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f0208-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="f0208-119"><a name="migrate"></a>Toohello nieuwe gateway-SKU's migreren</span><span class="sxs-lookup"><span data-stu-id="f0208-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="f0208-120">Als u met Hallo Resource Manager-implementatiemodel werkt, kunt u toohello nieuwe gateway-SKU's migreren.</span><span class="sxs-lookup"><span data-stu-id="f0208-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="f0208-121">Als u met het klassieke implementatiemodel hello werkt, u toohello niet overzetten nieuwe SKU's en moet in plaats daarvan toouse blijven Hallo verouderde SKU's.</span><span class="sxs-lookup"><span data-stu-id="f0208-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f0208-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0208-122">Next steps</span></span>

<span data-ttu-id="f0208-123">Voor meer informatie over Hallo nieuwe Gateway-SKU's, Zie [Gateway-SKU's](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="f0208-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="f0208-124">Zie voor meer informatie over configuratie-instellingen, [configuratie-instellingen over VPN-Gateway](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="f0208-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>