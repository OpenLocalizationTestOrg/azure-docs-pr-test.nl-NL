---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: PowerShell: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe virtuele toolink (vnet's) tooExpressRoute circuits netwerken met behulp van Hallo Resource Manager-implementatiemodel en PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit
> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure-CLI](howto-linkvnet-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-linkvnet-classic.md)
>

In dit artikel helpt u bij virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits koppelen via Hallo Resource Manager-implementatiemodel en PowerShell. Virtuele netwerken in Hallo kunnen zijn hetzelfde abonnement of een deel van een ander abonnement. Dit artikel leest u hoe tooupdate een virtueel netwerk koppelen. 

## <a name="before-you-begin"></a>Voordat u begint
* Installeer de nieuwste versie van de Hallo van hello Azure PowerShell-modules. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* Bekijk Hallo [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* U moet een actief ExpressRoute-circuit hebben. 
  * Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat Hallo-circuit inschakelen door de connectiviteitsprovider. 
  * Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd. Zie Hallo [routering configureren](expressroute-howto-routing-arm.md) artikel voor routering instructies. 
  * Zorg ervoor dat persoonlijke Azure-peering is geconfigureerd en actief Hallo BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.
  * Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht. Hallo-instructies te volgen[maken van een virtuele netwerkgateway voor ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Hallo GatewayType 'ExpressRoute' niet VPN maakt gebruik van een virtuele netwerkgateway voor ExpressRoute.

* U kunt een koppeling van too10 virtuele netwerken tooa standaard ExpressRoute-circuit. Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit. 

* U kunt een virtuele netwerken buiten de geopolitieke regio Hallo Hallo ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken tooyour ExpressRoute-circuit als u premium-invoegtoepassing voor ExpressRoute Hallo ingeschakeld. Controleer de Hallo [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit
Met behulp van de volgende cmdlet Hallo kunt u een virtueel netwerk gateway tooan ExpressRoute-circuit. Zorg ervoor dat Hallo virtuele netwerkgateway wordt gemaakt en is gereed voor het koppelen voordat u de cmdlet Hallo uitvoeren:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit
U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen. Hallo volgende afbeelding ziet u een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.

Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie. Elk van de afdelingen binnen de organisatie Hallo Hallo hun eigen abonnement kunt gebruiken voor het implementeren van hun services--, maar een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk kunnen delen. Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit. Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.

> [!NOTE]
> Verbindingen en bandbreedte kosten voor Hallo ExpressRoute-circuit is eigenaar van de toegepaste toohello-abonnement. Alle virtuele netwerken Hallo delen dezelfde bandbreedte.
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Beheer - circuit eigenaars en circuit gebruikers

Hallo 'circuiteigenaar' is een geautoriseerde gebruiker Power Hallo ExpressRoute-circuit resource. Hallo circuiteigenaar kunt autorisaties die kunnen worden ingewisseld door 'circuit gebruikers' maken. Circuit gebruikers kunnen eigenaren van het virtuele netwerk gateways die niet binnen hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit. Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).

Hallo circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment. Intrekken van een vergunning resulteert in alle koppeling verbindingen wordt verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.

### <a name="circuit-owner-operations"></a>Circuit eigenaar bewerkingen

**toocreate een autorisatie**

Hallo circuiteigenaar maakt een autorisatie. Dit resulteert in Hallo maken van een autorisatiesleutel die kan worden gebruikt door een gebruiker circuit tooconnect hun virtuele netwerk gateways toohello ExpressRoute-circuit. Een vergunning is geldig voor slechts één verbinding.

Hallo cmdlet fragment wordt getoond hoe na een vergunning toocreate:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Hallo antwoord toothis bevat autorisatiesleutel hello en status:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview autorisaties**

Hallo circuiteigenaar kunt alle machtigingen die zijn uitgegeven voor een bepaalde circuit door het uitvoeren van de volgende cmdlet Hallo bekijken:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd autorisaties**

Hallo circuiteigenaar kunt autorisaties toevoegen met behulp van de volgende cmdlet Hallo:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete autorisaties**

Hallo circuiteigenaar kunt intrekken/delete autorisaties toohello gebruiker door het uitvoeren van de volgende cmdlet Hallo:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Bewerkingen voor circuit-gebruikers

Hallo circuit gebruiker moet Hallo peer-ID en een autorisatiesleutel van Hallo circuiteigenaar. Hallo autorisatiesleutel is een GUID.

Peer-ID kan worden gecontroleerd vanuit Hallo volgende opdracht:

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**een verbindingsverificatie tooredeem**

Hallo circuitgebruikers kunt Hallo cmdlet tooredeem na een koppeling autorisatie uitvoeren:

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**een verbindingsverificatie toorelease**

U kunt een vergunning vrijgeven door Hallo-verbinding die is gekoppeld aan Hallo ExpressRoute-circuit toohello virtueel netwerk te verwijderen.

## <a name="modify-a-virtual-network-connection"></a>De verbinding van een virtueel netwerk wijzigen
U kunt bepaalde eigenschappen van een virtueel netwerkverbinding bijwerken. 

**tooupdate hello verbinding gewicht**

Het virtuele netwerk kan worden verbonden toomultiple ExpressRoute-circuits. Het foutbericht Hallo dezelfde voorvoegsel van meer dan één ExpressRoute-circuit. toochoose welke verbinding toosend-verkeer dat is bestemd voor dit voorvoegsel, kunt u *RoutingWeight* van een verbinding. Verkeer wordt verzonden op Hallo verbinding met de hoogste Hallo *RoutingWeight*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

Hallo reeks *RoutingWeight* too32000 0 is. Hallo-standaardwaarde is 0.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
