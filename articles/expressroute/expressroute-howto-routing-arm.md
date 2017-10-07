---
title: 'Hoe tooconfigure routering (peering) voor een ExpressRoute-circuit: Resource Manager: PowerShell: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Maken en wijzigen van de peering voor een ExpressRoute-circuit met PowerShell

In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel met behulp van PowerShell. U kunt ook controleren Hallo status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit. Als u wilt dat een andere methode toowork toouse met uw circuit, selecteert u een artikel in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure-CLI](howto-routing-cli.md)
> * [Video - persoonlijke peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - openbare peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft-peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Configuratievereisten

* U moet de meest recente versie Hallo van hello Azure Resource Manager PowerShell-cmdlets. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). 
* Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) pagina hello [routeringsvereisten](expressroute-routing.md) pagina en Hallo [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* U moet een actief ExpressRoute-circuit hebben. Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo cmdlets in dit artikel.

Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden. Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.

> [!IMPORTANT]
> We momenteel doen nog geen peerings geconfigureerd door serviceproviders via Hallo service management portal. Deze mogelijkheid zal binnenkort worden ingeschakeld. Neem contact op met uw serviceprovider voordat u BGP-peerings configureert.
> 
> 

U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren. U kunt peerings configureren in elke gewenste volgorde. Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien. 

## <a name="azure-private-peering"></a>Persoonlijke Azure-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit.

### <a name="toocreate-azure-private-peering"></a>toocreate persoonlijke Azure-peering

1. Importeer Hallo PowerShell-module voor ExpressRoute.

  Moet u het meest recente PowerShell installer Hallo van installeren [PowerShell Gallery](http://www.powershellgallery.com/) en hello Azure Resource Manager-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets. U moet toorun PowerShell als beheerder.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Importeer alle AzureRM.*-modules Hallo binnen Hallo bekende semantische versiebereik.

  ```powershell
  Import-AzureRM
  ```

  U kunt ook gewoon een bepaalde module binnen Hallo bekend bereik semantische versie importeren.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Meld u aan tooyour-account.

  ```powershell
  Login-AzureRmAccount
  ```

  Selecteer Hallo abonnement u wilt dat toocreate ExpressRoute-circuit.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Maak een ExpressRoute-circuit.

  Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het inrichten door de connectiviteitsprovider Hallo.

  Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.
3. Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld. Gebruik Hallo voorbeeld te volgen:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configureer persoonlijke Azure-peering voor Hallo circuit. Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:

  * Een/30 subnet voor de primaire koppeling Hallo. Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.
  * Een/30 subnet voor de secundaire koppeling Hallo. Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken. U kunt een persoonlijk AS-nummer voor deze peering gebruiken. Zorg dat u niet 65515 gebruikt.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.

  Gebruik Hallo voorbeeld tooconfigure Azure persoonlijke peering voor uw circuit te volgen:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview Azure persoonlijke peering details

U kunt configuratie-informatie krijgen met behulp van Hallo voorbeeld te volgen:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure configuratie van persoonlijke peering

U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken. In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 100 too500 bijgewerkt.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete persoonlijke Azure-peering

U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:

> [!WARNING]
> U moet ervoor zorgen dat alle virtuele netwerken losgekoppeld van Hallo ExpressRoute-circuit zijn voordat u dit voorbeeld. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Openbare Azure-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.

### <a name="toocreate-azure-public-peering"></a>toocreate openbare Azure-peering

1. Importeer Hallo PowerShell-module voor ExpressRoute.

  Moet u het meest recente PowerShell installer Hallo van installeren [PowerShell Gallery](http://www.powershellgallery.com/) en hello Azure Resource Manager-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets. U moet toorun PowerShell als beheerder.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Importeer alle AzureRM.*-modules Hallo binnen Hallo bekende semantische versiebereik.

  ```powershell
  Import-AzureRM
  ```

  U kunt ook gewoon een bepaalde module binnen Hallo bekend bereik semantische versie importeren.

  ```powershell
  Import-Module AzureRM.Network
```

  Meld u aan tooyour-account.

  ```powershell
  Login-AzureRmAccount
  ```

  Selecteer Hallo abonnement u wilt dat toocreate ExpressRoute-circuit.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Maak een ExpressRoute-circuit.

  Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het inrichten door de connectiviteitsprovider Hallo.

  Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.
3. Controleer Hallo ExpressRoute-circuit tooensure is ingericht en ook ingeschakeld. Gebruik Hallo voorbeeld te volgen:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configureer openbare Azure-peering voor Hallo circuit. Zorg ervoor dat u de volgende informatie voordat u verder Hallo hebt.

  * Een/30 subnet voor de primaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
  * Een/30 subnet voor de secundaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.

  Hallo na voorbeeld tooconfigure openbare peering voor uw circuit Azure uitvoeren

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview Azure openbare peering details

U kunt met behulp van de volgende cmdlet Hallo configuratiedetails krijgen:

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>configuratie van openbare peering Azure tooupdate

U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken. In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 200 too600 bijgewerkt.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete openbare Azure-peering

U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Microsoft-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit.

> [!IMPORTANT]
> Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Hallo Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd. Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit. Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft-peering

1. Importeer Hallo PowerShell-module voor ExpressRoute.

  Moet u het meest recente PowerShell installer Hallo van installeren [PowerShell Gallery](http://www.powershellgallery.com/) en hello Azure Resource Manager-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets. U moet toorun PowerShell als beheerder.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Importeer alle AzureRM.*-modules Hallo binnen Hallo bekende semantische versiebereik.

  ```powershell
  Import-AzureRM
  ```

  U kunt ook gewoon een bepaalde module binnen Hallo bekend bereik semantische versie importeren.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Meld u aan tooyour-account.

  ```powershell
  Login-AzureRmAccount
  ```

  Selecteer Hallo abonnement u wilt dat toocreate ExpressRoute-circuit.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Maak een ExpressRoute-circuit.

  Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het inrichten door de connectiviteitsprovider Hallo.

  Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.
3. Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld. Gebruik Hallo voorbeeld te volgen:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configureer Microsoft-peering voor Hallo circuit. Zorg ervoor dat er Hallo volgende informatie voordat u verder.

  * Een/30 subnet voor de primaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.
  * Een/30 subnet voor de secundaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken.
  * Geadverteerde voorvoegsels: U moet een lijst verstrekken van alle voorvoegsels die u van plan bent tooadvertise via Hallo BGP-sessie. Alleen openbare IP-adresvoorvoegsels worden geaccepteerd. Als u een reeks voorvoegsels toosend plant, kunt u een door komma's gescheiden lijst verzenden. Deze voorvoegsels moeten geregistreerde tooyou in een RIR / IRR.
  * **Optionele -** klant-ASN: als u voorvoegsels adverteert die niet zijn ingeschreven toohello peering als getal, kunt u Hallo opgeven als getal toowhich ze zijn geregistreerd.
  * Naam van Routeringsregister: Kunt u Hallo RIR / IRR met betrekking tot welke Hallo als number en prefixes zijn geregistreerd.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.

   Gebruik Hallo voorbeeld tooconfigure Microsoft-peering voor uw circuit te volgen:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>details van tooget Microsoft-peering

U kunt krijgen configuratiegegevens wilt weergeven Hallo voorbeeld te volgen:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configuratie van tooupdate Microsoft-peering

U kunt elk deel van Hallo-configuratie met Hallo volgt bijwerken:

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft-peering

U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Volgende stappen

Volgende stap, [koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md).

* Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).
* Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).
* Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.
