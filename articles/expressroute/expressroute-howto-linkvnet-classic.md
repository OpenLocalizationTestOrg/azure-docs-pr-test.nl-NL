---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: PowerShell: klassieke: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe virtuele toolink (vnet's) tooExpressRoute circuits netwerken met behulp van Hallo klassieke implementatiemodel en PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit met behulp van PowerShell (klassiek)
> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure-CLI](howto-linkvnet-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-linkvnet-classic.md)
>

In dit artikel helpt u virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits koppelen via Hallo klassieke implementatiemodel en PowerShell. Virtuele netwerken kunnen hetzelfde abonnement Hallo of zijn kan deel uitmaken van een ander abonnement.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Configuratievereisten
1. Moet u de meest recente versie Hallo van hello Azure PowerShell-modules. U kunt de meest recente PowerShell-modules Hallo downloaden van Hallo PowerShell sectie Hallo [pagina Azure Downloads](https://azure.microsoft.com/downloads/). Volg de instructies in Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor stapsgewijze instructies voor het tooconfigure uw computer toouse hello Azure PowerShell-modules.
2. U moet tooreview hello [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.
3. U moet een actief ExpressRoute-circuit hebben.
   * Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en vraag uw connectiviteitsprovider Hallo circuit inschakelen.
   * Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd. Zie Hallo [Configure routing](expressroute-howto-routing-classic.md) artikel voor routering instructies.
   * Zorg ervoor dat persoonlijke Azure-peering is geconfigureerd en actief Hallo BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.
   * U hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht. Hallo-instructies te volgen[een virtueel netwerk configureren voor ExpressRoute](expressroute-howto-vnet-portal-classic.md).

U kunt een koppeling van too10 virtuele netwerken tooan ExpressRoute-circuit. Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio. U kunt een groter aantal virtuele netwerken tooyour ExpressRoute-circuit koppelen of koppelen van virtuele netwerken die zich in andere geopolitieke regio's als u premium-invoegtoepassing voor ExpressRoute Hallo ingeschakeld. Controleer de Hallo [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit
U kunt een virtueel netwerk tooan ExpressRoute-circuit met behulp van de volgende cmdlet Hallo koppelen. Zorg ervoor dat Hallo virtuele netwerkgateway wordt gemaakt en is gereed voor het koppelen voordat u het Hallo-cmdlet uitvoert.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit
U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen. Hallo volgende afbeelding ziet u een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.

Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie. Alle Hallo afdelingen binnen Hallo organisatie kan hun eigen abonnement gebruiken voor het implementeren van hun services-- maar Hallo afdelingen een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk kan delen. Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit. Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.

> [!NOTE]
> Verbindingen en bandbreedte kosten voor speciale Hallo circuit zijn toegepaste toohello ExpressRoute-circuiteigenaar. Alle virtuele netwerken Hallo delen dezelfde bandbreedte.
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Beheer
Hallo *circuiteigenaar* is Hallo beheerder/CO-beheerder van het Hallo-abonnement in welke Hallo ExpressRoute circuit is gemaakt. Hallo circuiteigenaar kan machtigen beheerders/coadministrators van andere abonnementen, waarnaar wordt verwezen tooas *circuit gebruikers*, toouse Hallo dedicated circuit waarvan ze eigenaar. Circuit-gebruikers die geautoriseerd toouse Hallo organisatie ExpressRoute-circuit kan zijn koppelen Hallo virtuele netwerk in hun abonnement toohello ExpressRoute-circuit nadat ze zijn gemachtigd.

Hallo circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment. Intrekken van een vergunning leidt ertoe dat alle koppelingen worden verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.

### <a name="circuit-owner-operations"></a>Circuit eigenaar bewerkingen

**Maken van een vergunning**

Hallo circuiteigenaar machtigt Hallo beheerders van andere abonnementen toouse Hallo opgegeven circuit. Hallo beheerder van Hallo circuit (Contoso IT) kunt Hallo voorbeeld te volgen, Hallo beheerder van een ander abonnement (Dev-Test) toolink up tootwo virtuele netwerken toohello circuit. Hallo Contoso IT-beheerder maakt dit door op te geven Hallo Microsoft Dev-Test-ID. Hallo-cmdlet verzenden niet e toohello opgegeven Microsoft-ID. Hallo circuiteigenaar moet tooexplicitly melden Hallo andere eigenaar van het abonnement dat Hallo autorisatie is voltooid.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Machtigingen controleren**

Hallo circuiteigenaar kunt alle machtigingen die zijn uitgegeven voor een bepaalde circuit door het uitvoeren van de volgende cmdlet Hallo bekijken:

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Autorisaties bijwerken**

Hallo circuiteigenaar kunt autorisaties wijzigen met behulp van de volgende cmdlet Hallo:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Autorisaties verwijderen**

Hallo circuiteigenaar kunt intrekken/delete autorisaties toohello gebruiker door het uitvoeren van de volgende cmdlet Hallo:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Bewerkingen voor circuit-gebruikers

**Machtigingen controleren**

Hallo circuitgebruikers kunt autorisaties bekijken met behulp van de volgende cmdlet Hallo:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Wisselt autorisaties voor koppelingen**

Hallo circuitgebruikers kunt Hallo cmdlet tooredeem na een koppeling autorisatie uitvoeren:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Deze opdracht uitvoeren in het abonnement voor het virtuele netwerk Hallo Hallo zojuist gekoppeld:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).

