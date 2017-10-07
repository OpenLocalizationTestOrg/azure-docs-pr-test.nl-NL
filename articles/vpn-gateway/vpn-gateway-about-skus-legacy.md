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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Werken met virtuele netwerkgateway SKU's (verouderde SKU's)

In dit artikel bevat informatie over Hallo oudere (oude) virtuele netwerkgateway SKU's. Hallo legacy SKU's werkt nog steeds in beide implementatiemodellen voor VPN-gateways die al zijn gemaakt. Klassieke VPN-gateways gaan toouse Hallo verouderde SKU's, zowel voor gateways voor bestaande en nieuwe gateways. Bij het maken van nieuwe Resource Manager VPN gateways, gebruik Hallo nieuwe gateway-SKU's. Zie voor informatie over Hallo nieuwe SKU's, [over VPN-Gateway](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>Gateway-SKU's

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>Geschatte geaggregeerde doorvoer per SKU

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>Ondersteunde configuraties op SKU- en VPN-type

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Een gateway (wijziging een gateway-SKU) vergroten of verkleinen

U kunt het formaat van een gateway-SKU binnen Hallo dezelfde SKU-serie. Als u een standaard SKU hebt, kunt u bijvoorbeeld tooa HighPerformance SKU grootte. U kunt geen grootte van uw VPN-gateways tussen Hallo oude SKU's en nieuwe SKU families Hallo. U kunt niet bijvoorbeeld gaan van een standaard SKU tooa VpnGw2 SKU. 

tooresize een gateway-SKU voor Hallo klassieke implementatiemodel, gebruik Hallo volgende opdracht:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize gateway SKU voor Resource Manager-implementatiemodel, Hallo Hallo volgende opdracht gebruiken:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Toohello nieuwe gateway-SKU's migreren

Als u met Hallo Resource Manager-implementatiemodel werkt, kunt u toohello nieuwe gateway-SKU's migreren. Als u met het klassieke implementatiemodel hello werkt, u toohello niet overzetten nieuwe SKU's en moet in plaats daarvan toouse blijven Hallo verouderde SKU's.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Volgende stappen

Voor meer informatie over Hallo nieuwe Gateway-SKU's, Zie [Gateway-SKU's](vpn-gateway-about-vpngateways.md#gwsku).

Zie voor meer informatie over configuratie-instellingen, [configuratie-instellingen over VPN-Gateway](vpn-gateway-about-vpn-gateway-settings.md).