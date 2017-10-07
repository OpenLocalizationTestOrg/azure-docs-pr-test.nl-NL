---
title: 'Hoe tooconfigure routering (peering) voor een ExpressRoute-circuit: Azure: klassieke | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Maken en wijzigen van de peering voor een ExpressRoute-circuit (klassiek)
> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure-CLI](howto-routing-cli.md)
> * [Video - persoonlijke peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - openbare peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft-peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-routing-classic.md)
> 

Dit artikel begeleidt u bij Hallo stappen toocreate en beheren van routeringsconfiguratie voor een ExpressRoute-circuit met PowerShell en Hallo klassieke implementatiemodel. Hallo stappen hieronder ziet u ook hoe toocheck Hallo status, bijwerken, of verwijder en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Configuratievereisten
* U moet de meest recente versie Hallo van hello Azure Service Management (SM) PowerShell-cmdlets. Zie voor meer informatie [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview).  
* Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) pagina hello [routeringsvereisten](expressroute-routing.md) pagina en Hallo [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
* U moet een actief ExpressRoute-circuit hebben. Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo cmdlets die hieronder worden beschreven.

> [!IMPORTANT]
> Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden. Als u gebruikmaakt van een serviceprovider die beheerde Laag-3-services aanbiedt (meestal een IPVPN, zoals MPLS), zal de connectiviteitsprovider routering voor u configureren en beheren.
> 
> 

U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren. U kunt peerings configureren in elke gewenste volgorde. Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Meld u bij tooyour Azure-account en een abonnement selecteren
1. Open de PowerShell-console met verhoogde rechten en tooyour-account koppelen. Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:

        Login-AzureRmAccount

2. Controleer de abonnementen Hallo voor Hallo-account.

        Get-AzureRmSubscription

3. Als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u wilt dat toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Gebruik vervolgens Hallo cmdlet tooadd na uw Azure-abonnement tooPowerShell Hallo klassieke implementatiemodel.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Persoonlijke Azure-peering
Deze sectie bevat instructies over hoe toocreate, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit. 

### <a name="toocreate-azure-private-peering"></a>toocreate persoonlijke Azure-peering
1. **Importeer Hallo PowerShell-module voor ExpressRoute.**
   
    U moet hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets. Voer Hallo volgende opdrachten tooimport hello Azure en een ExpressRoute-modules in Hallo PowerShell-sessie.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Maak een ExpressRoute-circuit.**
   
    Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en laat het inrichten door de connectiviteitsprovider Hallo. Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert volgt u onderstaande Hallo-instructies. 
3. **Controleer Hallo ExpressRoute-circuit tooensure die deze is ingericht.**
   
    Als Hallo ExpressRoute-circuit is ingericht en ook is ingeschakeld, moet u eerst toosee controleren. Zie Hallo voorbeeld hieronder.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Zorg ervoor dat Hallo circuit ingericht en ingeschakeld bevat. Als dit niet het geval is, samen met uw provider connectiviteit tooget uw circuit toohello vereist toestand en status.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configureer persoonlijke Azure-peering voor Hallo circuit.**
   
    Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:
   
   * Een/30 subnet voor de primaire koppeling Hallo. Dit mag geen deel uitmaken van een adresruimte die is gereserveerd voor virtuele netwerken.
   * Een/30 subnet voor de secundaire koppeling Hallo. Dit mag geen deel uitmaken van een adresruimte die is gereserveerd voor virtuele netwerken.
   * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
   * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken. U kunt een persoonlijk AS-nummer voor deze peering gebruiken. Zorg dat u niet 65515 gebruikt.
   * Een MD5-hash als u ervoor toouse een kiest. **Dit is optioneel**.
     
    U kunt uitvoeren Hallo cmdlet tooconfigure persoonlijke Azure-peering voor uw circuit te volgen.
     
        Nieuwe AzureBGPPeering - AccessType persoonlijke - ServiceKey ' *** ' - PrimaryPeerSubnet '10.0.0.0/30' - SecondaryPeerSubnet '10.0.0.4/30' - PeerAsn 1234 - VlanId 100
     
    U kunt Hallo onderstaande cmdlet gebruiken als u een MD5-hash toouse kiest.
     
        Nieuwe AzureBGPPeering - AccessType persoonlijke - ServiceKey ' *** ' - PrimaryPeerSubnet '10.0.0.0/30' - SecondaryPeerSubnet '10.0.0.4/30' - PeerAsn 1234 - VlanId 100 - SharedKey 'A1B2C3D4'
     
     > [!IMPORTANT]
     > Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure persoonlijke peering details
U kunt met behulp van de volgende cmdlet Hallo configuratiedetails ophalen

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure configuratie van persoonlijke peering
U kunt elk deel van Hallo-configuratie met behulp van de volgende cmdlet Hallo bijwerken. In onderstaande Hallo voorbeeld, wordt Hallo VLAN-ID van het circuit Hallo van 100 too500 bijgewerkt.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete persoonlijke Azure-peering
U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo.

> [!WARNING]
> U moet ervoor zorgen dat alle virtuele netwerken losgekoppeld van Hallo ExpressRoute-circuit zijn voordat u deze cmdlet uitvoert. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Openbare Azure-peering
Deze sectie bevat instructies over hoe toocreate, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.

### <a name="toocreate-azure-public-peering"></a>toocreate openbare Azure-peering
1. **Importeer Hallo PowerShell-module voor ExpressRoute.**
   
    U moet hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets. Voer Hallo volgende opdrachten tooimport hello Azure en een ExpressRoute-modules in Hallo PowerShell-sessie. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Een ExpressRoute-circuit maken**
   
    Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en laat het inrichten door de connectiviteitsprovider Hallo. Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable openbare peering voor u Azure aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert volgt u onderstaande Hallo-instructies.
3. **Deze is voorzien van ExpressRoute-circuit tooensure controleren**
   
    Als Hallo ExpressRoute-circuit is ingericht en ook is ingeschakeld, moet u eerst toosee controleren. Zie Hallo voorbeeld hieronder.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Zorg ervoor dat Hallo circuit ingericht en ingeschakeld bevat. Als dit niet het geval is, samen met uw provider connectiviteit tooget uw circuit toohello vereist toestand en status.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configureer openbare Azure-peering voor Hallo circuit**
   
    Zorg ervoor dat u de volgende informatie voordat u verder Hallo hebt.
   
   * Een/30 subnet voor de primaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
   * Een/30 subnet voor de secundaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
   * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
   * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken.
   * Een MD5-hash als u ervoor toouse een kiest. **Dit is optioneel**.
     
    Kunt u de volgende cmdlet tooconfigure openbare Azure-peering voor uw circuit Hallo uitvoeren
     
        Nieuwe AzureBGPPeering - AccessType openbare - ServiceKey ' *** ' - PrimaryPeerSubnet '131.107.0.0/30' - SecondaryPeerSubnet '131.107.0.4/30' - PeerAsn 1234 - VlanId 200
     
    U kunt Hallo onderstaande cmdlet gebruiken als u een MD5-hash toouse kiezen
     
        Nieuwe AzureBGPPeering - AccessType openbare - ServiceKey ' *** ' - PrimaryPeerSubnet '131.107.0.0/30' - SecondaryPeerSubnet '131.107.0.4/30' - PeerAsn 1234 - VlanId 200 - SharedKey 'A1B2C3D4'
     
     > [!IMPORTANT]
     > Zorg dat u uw AS-nummer als peering-ASN opgeeft en niet als klant-ASN.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview Azure openbare peering details
U kunt met behulp van de volgende cmdlet Hallo configuratiedetails ophalen

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>configuratie van openbare peering Azure tooupdate
U kunt elk deel van Hallo-configuratie met behulp van de volgende cmdlet Hallo bijwerken

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Hallo VLAN-ID van het circuit Hallo wordt van 200 too600 in Hallo bovenstaande voorbeeld bijgewerkt.

### <a name="toodelete-azure-public-peering"></a>toodelete openbare Azure-peering
U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Microsoft-peering
Deze sectie bevat instructies over hoe toocreate, verkrijgen, bijwerken en verwijderen van configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit. 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft-peering
1. **Importeer Hallo PowerShell-module voor ExpressRoute.**
   
    U moet hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets. Voer Hallo volgende opdrachten tooimport hello Azure en een ExpressRoute-modules in Hallo PowerShell-sessie.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Een ExpressRoute-circuit maken**
   
    Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en laat het inrichten door de connectiviteitsprovider Hallo. Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert volgt u onderstaande Hallo-instructies.
3. **Deze is voorzien van ExpressRoute-circuit tooensure controleren**
   
    Als Hallo ExpressRoute-circuit ingericht en ingeschakeld is, moet u eerst toosee controleren.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Zorg ervoor dat Hallo circuit ingericht en ingeschakeld bevat. Als dit niet het geval is, samen met uw provider connectiviteit tooget uw circuit toohello vereist toestand en status.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configureer Microsoft-peering voor Hallo circuit**
   
    Zorg ervoor dat er Hallo volgende informatie voordat u verder.
   
   * Een/30 subnet voor de primaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.
   * Een/30 subnet voor de secundaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.
   * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
   * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken.
   * Geadverteerde voorvoegsels: U moet een lijst verstrekken van alle voorvoegsels die u van plan bent tooadvertise via Hallo BGP-sessie. Alleen openbare IP-adresvoorvoegsels worden geaccepteerd. Als u van plan een reeks voorvoegsels toosend bent, kunt u een door komma's gescheiden lijst verzenden. Deze voorvoegsels moeten geregistreerde tooyou in een RIR / IRR.
   * Klant-ASN: Als u voorvoegsels die niet zijn ingeschreven toohello peering als getal worden geadverteerd, kunt u Hallo opgeven als getal toowhich die ze zijn geregistreerd. **Dit is optioneel**.
   * Naam van Routeringsregister: Kunt u Hallo RIR / IRR met betrekking tot welke Hallo als number en prefixes zijn geregistreerd.
   * Een MD5-hash, als u ervoor toouse een kiest. **Dit is optioneel.**
     
    Kunt u de volgende cmdlet tooconfigure Microsoft pering voor uw circuit Hallo uitvoeren
     
        Nieuwe AzureBGPPeering - AccessType Microsoft - ServiceKey ' *** ' - PrimaryPeerSubnet '131.107.0.0/30' - SecondaryPeerSubnet '131.107.0.4/30' - VlanId 300 - PeerAsn 1234 - CustomerAsn. 2245 - AdvertisedPublicPrefixes '123.0.0.0/30' - RoutingRegistryName 'ARIN' - SharedKey 'A1B2C3D4'

### <a name="tooview-microsoft-peering-details"></a>details van tooview Microsoft-peering
U kunt met behulp van de volgende cmdlet Hallo configuratiedetails ophalen.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>configuratie van tooupdate Microsoft-peering
U kunt elk deel van Hallo-configuratie met behulp van de volgende cmdlet Hallo bijwerken.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft-peering
U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Volgende stappen
Vervolgens [koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md).

* Zie voor meer informatie over werkstromen [ExpressRoute-werkstromen](expressroute-workflows.md).
* Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).

