---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: CLI: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe virtuele toolink (vnet's) tooExpressRoute circuits netwerken met behulp van Hallo Resource Manager-implementatiemodel en CLI.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit met CLI

In dit artikel helpt u bij virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits met CLI koppelen. met Azure CLI toolink Hallo virtuele netwerken worden gemaakt met behulp van Hallo Resource Manager-implementatiemodel. Ze kunnen zijn in Hallo hetzelfde abonnement of een deel van een ander abonnement. Als u een andere methode tooconnect toouse uw VNet tooan ExpressRoute-circuit wilt, kunt u een artikel van Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure-CLI](howto-linkvnet-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Configuratievereisten

* U moet de meest recente versie Hallo van Hallo-opdrachtregelinterface (CLI). Zie voor meer informatie [2.0 voor Azure CLI installeren](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* U moet tooreview hello [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* U moet een actief ExpressRoute-circuit hebben. 
  * Hallo-instructies te volgen[maken van een ExpressRoute-circuit](howto-circuit-cli.md) en laat Hallo-circuit inschakelen door de connectiviteitsprovider. 
  * Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd. Zie Hallo [routering configureren](howto-routing-cli.md) artikel voor routering instructies. 
  * Zorg ervoor dat de persoonlijke Azure-peering is geconfigureerd. Hallo BGP-peering tussen uw netwerk en Microsoft moet zodat u kunt end-to-end-connectiviteit inschakelen.
  * Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht. Hallo-instructies te volgen[configureren van een virtuele netwerkgateway voor ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Ervoor toouse worden `--gateway-type ExpressRoute`.

* U kunt een koppeling van too10 virtuele netwerken tooa standaard ExpressRoute-circuit. Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit. 

* Als u premium-invoegtoepassing voor ExpressRoute Hallo inschakelt, kunt u een virtueel netwerk buiten de geopolitieke regio Hallo Hallo ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken tooyour ExpressRoute-circuit. Zie voor meer informatie over de premium-invoegtoepassing Hallo Hallo [Veelgestelde vragen over](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit

Met behulp van Hallo voorbeeld kunt u een virtueel netwerk gateway tooan ExpressRoute-circuit. Zorg ervoor dat Hallo virtuele netwerkgateway wordt gemaakt en is gereed voor het koppelen voordat u Hallo-opdracht uitvoert.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit

U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen. Hallo afbeelding hieronder ziet een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.

Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie. Elk van de afdelingen binnen de organisatie Hallo Hallo hun eigen abonnement kunt gebruiken voor het implementeren van hun services--, maar een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk kunnen delen. Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit. Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.

> [!NOTE]
> Verbindingen en bandbreedte kosten voor speciale Hallo circuit zijn toegepaste toohello ExpressRoute-Circuiteigenaar. Alle virtuele netwerken Hallo delen dezelfde bandbreedte.
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Beheer - Circuit eigenaars en Circuit gebruikers

Hallo 'Circuiteigenaar' is een geautoriseerde gebruiker Power Hallo ExpressRoute-circuit resource. Hallo Circuiteigenaar kunt autorisaties die kunnen worden ingewisseld door 'Circuit gebruikers' maken. Circuit gebruikers kunnen eigenaren van het virtuele netwerk gateways die niet binnen hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit. Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).

Hallo Circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment. Wanneer een vergunning wordt ingetrokken, worden alle koppeling verbindingen verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.

### <a name="circuit-owner-operations"></a>Circuit eigenaar bewerkingen

**toocreate een autorisatie**

Hallo Circuiteigenaar maakt een autorisatie, die wordt gemaakt van een autorisatiesleutel die kan worden gebruikt door een tooconnect Circuitgebruikers hun virtuele netwerk gateways toohello ExpressRoute-circuit. Een vergunning is geldig voor slechts één verbinding.

Hallo volgende voorbeeld wordt getoond hoe toocreate een vergunning:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

antwoord Hallo bevat Hallo autorisatiesleutel en de status:

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview autorisaties**

Hallo Circuiteigenaar kunt bekijken alle autorisaties die op een bepaalde circuit zijn uitgegeven door Hallo volgt uitgevoerd:

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd autorisaties**

Hallo Circuiteigenaar kunt autorisaties toevoegen met behulp van Hallo voorbeeld te volgen:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete autorisaties**

Hallo Circuiteigenaar kunt intrekken/delete autorisaties toohello gebruiker door te voeren Hallo voorbeeld te volgen:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Bewerkingen voor circuit-gebruikers

Hallo Circuitgebruikers nodig Hallo peer-ID en een autorisatiesleutel van Hallo Circuiteigenaar. Hallo autorisatiesleutel is een GUID.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**een verbindingsverificatie tooredeem**

Hallo Circuitgebruikers kunt Hallo voorbeeld tooredeem na een koppeling autorisatie uitvoeren:

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**een verbindingsverificatie toorelease**

U kunt een vergunning vrijgeven door Hallo-verbinding die is gekoppeld aan Hallo ExpressRoute-circuit toohello virtueel netwerk te verwijderen.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
