---
title: 'Maken en een ExpressRoute-circuit wijzigen: PowerShell: klassieke Azure Portal | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en een ExpressRoute-circuit inrichten. Dit artikel ziet u ook hoe toocheck Hallo status, bijwerken, of verwijderen en uw circuit inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Maken en een ExpressRoute-circuit met behulp van PowerShell (klassiek) wijzigen
> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure-CLI](howto-circuit-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-circuit-classic.md)
>

Dit artikel begeleidt u bij Hallo stappen toocreate een Azure ExpressRoute-circuit met PowerShell-cmdlets en Hallo klassieke implementatiemodel. Dit artikel leest u hoe toocheck Hallo status, bijwerken, of verwijderen en een ExpressRoute-circuit inrichting ervan ongedaan.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Voordat u begint
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>Step 1. Hallo-vereisten en werkstroom artikelen controleren
Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>Stap 2. De meest recente versies Hallo van hello Azure Service Management (SM) PowerShell-modules installeren
Volg de instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview) voor stapsgewijze instructies voor het tooconfigure uw computer toouse hello Azure PowerShell-modules.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>Stap 3. Meld u bij tooyour Azure-account en een abonnement selecteren
1. Open de PowerShell-console met verhoogde rechten en tooyour-account koppelen. Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:

        Login-AzureRmAccount

2. Controleer de abonnementen Hallo voor Hallo-account.

        Get-AzureRmSubscription

3. Als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u wilt dat toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Gebruik vervolgens Hallo cmdlet tooadd na uw Azure-abonnement tooPowerShell Hallo klassieke implementatiemodel.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Maken en een ExpressRoute-circuit inrichten
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>Step 1. Hallo PowerShell-modules importeren voor ExpressRoute
 Als u dit nog niet hebt gedaan, moet u hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets. Importeren van modules Hallo Hallo locatie die ze waren geïnstalleerd tooon uw lokale computer. Afhankelijk van de methode Hallo u tooinstall Hallo modules gebruikt, Hallo locatie mogelijk anders dan Hallo volgende voorbeeld wordt getoond. Hallo voorbeeld desgewenst wijzigen.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>Stap 2. Hallo-lijst met ondersteunde providers, locaties en bandbreedten
Voordat u een ExpressRoute-circuit maken, moet u Hallo lijst met ondersteunde connectiviteitsproviders, locaties en bandbreedte-opties.

PowerShell-cmdlet Hallo `Get-AzureDedicatedCircuitServiceProvider` retourneert deze informatie, die u in latere stappen:

    Get-AzureDedicatedCircuitServiceProvider

Controleer de toosee als uw connectiviteitsprovider daar wordt vermeld. Maak een notitie van de volgende informatie omdat u hebt deze later nodig bij het maken van een circuit Hallo:

* Naam
* PeeringLocations
* BandwidthsOffered

U bent nu klaar toocreate een ExpressRoute-circuit.         

### <a name="step-3-create-an-expressroute-circuit"></a>Stap 3. Een ExpressRoute-circuit maken
Hallo volgende voorbeeld ziet u hoe toocreate een 200 Mbps-ExpressRoute-circuit via Equinix in Silicon Valley. Als u een andere provider en andere instellingen gebruikt, vervangt u die informatie door wanneer u uw aanvraag.

> [!IMPORTANT]
> Uw ExpressRoute-circuit worden gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend. Zorg ervoor dat u deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.
> 
> 

Hallo Hier volgt een voorbeeld van de aanvraag voor een nieuwe servicesleutel:

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

Of als u een ExpressRoute-circuit met premium-invoegtoepassing voor Hallo toocreate wilt, gebruik Hallo voorbeeld te volgen. Raadpleeg toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


Hallo-antwoord bevat de servicesleutel Hallo. U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende Hallo:

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>Stap 4. Lijst van alle Hallo ExpressRoute-circuits
U kunt uitvoeren Hallo `Get-AzureDedicatedCircuit` opdracht tooget een lijst met alle Hallo ExpressRoute-circuits die u hebt gemaakt:

    Get-AzureDedicatedCircuit

antwoord Hallo zijn iets dergelijks toohello voorbeeld te volgen:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo `Get-AzureDedicatedCircuit` cmdlet. Hallo aanroepen zonder parameters maken een lijst met alle Hallo circuits. De sleutel van uw service wordt weergegeven in Hallo *ServiceKey* veld.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende Hallo:

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>Stap 5. Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden
*ServiceProviderProvisioningState* bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde. *Status* Hallo status biedt op Hallo Microsoft aan clientzijde. Zie voor meer informatie over het circuit inrichtingstatuswaarden hello [werkstromen](expressroute-workflows.md#expressroute-circuit-provisioning-states) artikel.

Bij het maken van nieuwe ExpressRoute-circuit liggen Hallo circuit Hallo status te volgen:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Hallo circuit gaat toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Een ExpressRoute-circuit moet zijn Hallo status voor u toobe kunnen toouse na het:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>Stap 6. Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren
Dit laat u weten wanneer uw provider uw circuit is ingeschakeld. Nadat het Hallo-circuit is geconfigureerd, *ServiceProviderProvisioningState* weergegeven als *ingericht* zoals weergegeven in Hallo voorbeeld te volgen:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>Stap 7. Maken van uw configuratie van de routering
Raadpleeg toohello [routeringsconfiguratie voor ExpressRoute-circuit (maken en wijzigen van circuit peerings)](expressroute-howto-routing-classic.md) artikel voor stapsgewijze instructies.

> [!IMPORTANT]
> Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden. Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>Stap 8. Koppelen van een virtueel netwerk tooan ExpressRoute-circuit
Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit. Raadpleeg te[koppelen ExpressRoute-circuits toovirtual netwerken](expressroute-howto-linkvnet-classic.md) voor stapsgewijze instructies. Als u een virtueel netwerk met het klassieke implementatiemodel Hallo voor ExpressRoute toocreate moet, Zie [een virtueel netwerk maken voor ExpressRoute](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Hallo-status van een ExpressRoute-circuit ophalen
U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo `Get-AzureCircuit` cmdlet. Hallo aanroepen zonder parameters maken een lijst met alle Hallo circuits.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

U kunt de informatie op een specifieke ExpressRoute-circuit opvragen door Hallo servicesleutel doorgeven als een aanroep van de parameter toohello.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van Hallo voorbeeld te volgen:

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Wijzigen van een ExpressRoute-circuit
U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.

U kunt doen Hallo zonder uitvaltijd te volgen:

* In- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.
* Hallo-bandbreedte verhoging van uw ExpressRoute-circuit mits capaciteit beschikbaar op Hallo-poort. Houd er rekening mee dat Hallo bandbreedte van een circuit downgraden wordt niet ondersteund. 
* Hallo softwarelicentiecontrole plan van gegevens Datalimiet tooUnlimited gegevens wijzigen. Houd er rekening mee dat veranderende Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.
* U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.

Raadpleeg toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie over limieten en beperkingen.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium-invoegtoepassing
U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit inschakelen met behulp van de volgende PowerShell-cmdlet Hallo:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

Het circuit hebt nu Hallo ExpressRoute premium-invoegtoepassing voor functies die worden ingeschakeld. Houd er rekening mee dat we facturering voor Hallo premium-invoegtoepassing mogelijkheid start zodra Hallo-opdracht met succes is uitgevoerd.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium-invoegtoepassing
> [!IMPORTANT]
> Deze bewerking kan mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.
> 
> 

#### <a name="considerations"></a>Overwegingen

* U moet ervoor zorgen dat het aantal virtuele netwerken gekoppelde toohello circuit Hallo minder dan 10 voordat u van premium toostandard downgraden. Als u dit doet, uw aanvraag bijwerken mislukt en u zult gefactureerd Hallo Premietarieven.
* U moet alle virtuele netwerken in andere geopolitieke regio's ontkoppelen. Als u dit doet, uw aanvraag bijwerken mislukt en u zult gefactureerd Hallo Premietarieven.
* De routetabel moet minder dan 4000 routes voor persoonlijke peering. Uw tabel route is groter dan 4000 routes, Hallo BGP-sessie wordt als totdat Hallo aantal geadverteerde voorvoegsels daaronder 4.000 won't worden ingeschakeld.

#### <a name="disable-hello-premium-add-on"></a>Premium-invoegtoepassing voor Hallo uitschakelen
U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit uitschakelen met behulp van de volgende PowerShell-cmdlet Hallo:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>bandbreedte tooupdate hello ExpressRoute-circuit
Controleer de Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor ondersteunde bandbreedte-opties voor uw provider. U kunt de grootte die groter is dan Hallo grootte van uw bestaande circuit zolang Hallo fysieke poort (waarop uw circuit is gemaakt) kunnen verzamelen.

> [!IMPORTANT]
> Mogelijk hebt u toorecreate hello ExpressRoute-circuit als er onvoldoende capaciteit op de bestaande poort Hallo. U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.
>
> U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren. Downgraden bandbreedte, moet u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.
> 
> 

#### <a name="resize-a-circuit"></a>Een circuit vergroten of verkleinen

Nadat u welke grootte die u nodig hebt besluit, kunt u uw circuit Hallo opdracht tooresize volgende gebruiken:

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Uw circuit wordt zijn grote Hallo Microsoft zijde. U moet contact opnemen met uw connectiviteit provider tooupdate-configuraties van hun kant toomatch deze wijziging. Opmerking dat we start u facturering voor Hallo bandbreedte optie vanaf dit punt op bijgewerkt.

Als u de volgende fout bij het verhogen van de bandbreedte van het circuit Hallo Hallo ziet, betekent dit er is onvoldoende bandbreedte links op Hallo van de fysieke poort waarop uw bestaande circuit is gemaakt. U hebt toodelete dit circuit en een nieuwe circuit Hallo grootte die u moet maken. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Opheffen van inrichting en een ExpressRoute-circuit verwijderen

### <a name="considerations"></a>Overwegingen

* U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit voor deze bewerking toosucceed ontkoppelen. Controleer toosee als er geen virtuele netwerken die zijn gekoppeld toohello circuit als deze bewerking is mislukt.
* Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht** moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant. We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.
* Als serviceprovider Hallo heeft gemaakt Hallo circuit (Hallo serviceprovider Inrichtingsstatus te is ingesteld**niet ingericht**) kunt u Hallo circuit verwijderen. Hiermee stopt u facturering voor Hallo circuit.

#### <a name="delete-a-circuit"></a>Een circuit verwijderen

U kunt uw ExpressRoute-circuit verwijderen door het uitvoeren van de volgende opdracht Hallo:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Volgende stappen
Nadat u het circuit hebt gemaakt, moet u Hallo te volgen:

* [Maken en aanpassen van routering voor ExpressRoute-circuit](expressroute-howto-routing-classic.md)
* [Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md)

