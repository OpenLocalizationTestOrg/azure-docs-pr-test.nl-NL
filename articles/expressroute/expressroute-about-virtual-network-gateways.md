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
# <a name="about-virtual-network-gateways-for-expressroute"></a>Virtuele netwerkgateways voor ExpressRoute
Een virtuele netwerkgateway wordt gebruikt toosend netwerkverkeer tussen virtuele netwerken van Azure en lokale locaties. Wanneer u een ExpressRoute-verbinding configureert, moet u maken en configureren van een virtuele netwerkgateway en een verbinding met virtual network gateway.

Wanneer u een gateway voor een virtueel netwerk maakt, geeft u verschillende instellingen op. Een van de instellingen Hallo vereist geeft aan of Hallo gateway wordt gebruikt voor ExpressRoute of Site-naar-Site VPN-verkeer. Hallo Resource Manager-implementatiemodel, Hallo-instelling is '-GatewayType'.

Wanneer netwerkverkeer op een persoonlijke verbinding die wordt verzonden, gebruikt u het Gatewaytype Hallo 'ExpressRoute'. Dit is ook bedoeld tooas een ExpressRoute-gateway. Wanneer netwerkverkeer verzonden versleutelde via openbaar Internet hello, gebruikt u Gatewaytype Hallo 'VPN-'. Dit is bedoeld tooas een VPN-gateway. Site-naar-site-, punt-naar-site- en VNet-naar-VNet-verbindingen gebruiken allemaal een VPN-gateway.

Elk virtueel netwerk kan maar één virtuele netwerkgateway per type gateway hebben. U kunt voor een virtueel netwerk bijvoorbeeld één gateway gebruiken die -GatewayType Vpn gebruikt en één die -GatewayType ExpressRoute gebruikt. Dit artikel is gericht op Hallo ExpressRoute virtuele netwerkgateway.

## <a name="gwsku"></a>Gateway-SKU's
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Als u wilt dat tooupgrade uw gateway tooa krachtiger Hallo gateway-SKU, in de meeste gevallen kunt u 'Formaat AzureRmVirtualNetworkGateway' PowerShell-cmdlet. Dit werkt voor upgrades tooStandard en HighPerformance SKU's. Tooupgrade toohello UltraPerformance SKU, u moet echter toorecreate Hallo gateway.

### <a name="aggthroughput"></a>Geschatte geaggregeerde doorvoer per gateway-SKU
Hallo volgende tabel toont Hallo gatewaytypen en Hallo geschatte geaggregeerde doorvoer. Deze tabel is van toepassing tooboth Hallo Resource Manager en de klassieke implementatiemodellen.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Doorvoer van de toepassing afhankelijk is van meerdere factoren, zoals Hallo end-to-end-latentie, en het Hallo-nummer van het verkeer stroomt Hallo toepassing wordt geopend. Hallo getallen in Hallo tabel vertegenwoordigen Hallo bovengrens theorectically, kunt u de toepassing hello bereiken in een omgeving met ideaal. 
> 
>

## <a name="resources"></a>REST-API's en PowerShell-cmdlets
Zie voor aanvullende technische bronnen en specifieke syntaxis vereisten bij het gebruik van REST-API's en PowerShell-cmdlets voor gateway-configuraties van virtuele netwerken, Hallo pagina's te volgen:

| **Klassiek** | **Resource Manager** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [REST API](https://msdn.microsoft.com/library/jj154113.aspx) |[REST API](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Volgende stappen
Zie [overzicht van ExpressRoute](expressroute-introduction.md) voor meer informatie over beschikbare verbinding configuraties. 

