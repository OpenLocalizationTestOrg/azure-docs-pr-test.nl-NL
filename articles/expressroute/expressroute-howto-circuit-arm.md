---
title: 'Maken en een ExpressRoute-circuit wijzigen: PowerShell: Azure Resource Manager | Microsoft Docs'
description: Dit artikel wordt beschreven hoe toocreate, inrichten, controleren, bijwerken, verwijderen en een ExpressRoute-circuit inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Maken en een ExpressRoute-circuit met PowerShell wijzigen
> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure-CLI](howto-circuit-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-circuit-classic.md)
>

Dit artikel wordt beschreven hoe toocreate een Azure ExpressRoute-circuit met behulp van PowerShell-cmdlets en hello Azure Resource Manager-implementatiemodel. Dit artikel ziet u ook hoe toocheck Hallo status van het Hallo-circuit, bijwerken of verwijderen en deze inrichting ervan ongedaan.

## <a name="before-you-begin"></a>Voordat u begint
* Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets. Zie voor meer informatie [overzicht van Azure PowerShell](/powershell/azure/overview).
* Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.


## <a name="create-and-provision-an-expressroute-circuit"></a>Maken en een ExpressRoute-circuit inrichten
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Meld u aan tooyour Azure-account en uw abonnement te selecteren
toobegin uw configuratie, aanmelden tooyour Azure-account. Gebruik Hallo volgen voorbeelden toohelp die u verbinding kunt maken:

```powershell
Login-AzureRmAccount
```

Controleer Hallo abonnementen voor Hallo-account:

```powershell
Get-AzureRmSubscription
```

Hallo-abonnement dat u wilt dat een ExpressRoute-circuit voor toocreate selecteren:

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Hallo-lijst met ondersteunde providers, locaties en bandbreedten
Voordat u een ExpressRoute-circuit maken, moet u Hallo lijst met ondersteunde connectiviteitsproviders, locaties en bandbreedte-opties.

PowerShell-cmdlet Hallo **Get-AzureRmExpressRouteServiceProvider** retourneert deze informatie, die u in latere stappen:

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Controleer de toosee als uw connectiviteitsprovider daar wordt vermeld. Noteer Hallo informatie te volgen. U hebt deze later nodig bij het maken van een circuit.

* Naam
* PeeringLocations
* BandwidthsOffered

U bent nu klaar toocreate een ExpressRoute-circuit.   

### <a name="3-create-an-expressroute-circuit"></a>3. Een ExpressRoute-circuit maken
Als u nog een resourcegroep hebt, moet u een maken voordat u uw ExpressRoute-circuit maken. U kunt dit doen door het uitvoeren van de volgende opdracht Hallo:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


Hallo volgende voorbeeld ziet u hoe toocreate een 200 Mbps-ExpressRoute-circuit via Equinix in Silicon Valley. Als u een andere provider en andere instellingen gebruikt, vervangt u die informatie door wanneer u uw aanvraag. Hallo Hier volgt een voorbeeld van de aanvraag voor een nieuwe servicesleutel:

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Zorg ervoor dat u de juiste SKU-laag Hallo en SKU-serie opgeeft:

* SKU-laag bepaalt of een standaard ExpressRoute of een premium-invoegtoepassing voor ExpressRoute is ingeschakeld. U kunt opgeven *standaard* tooget Hallo standaard SKU of *Premium* voor Hallo premium-invoegtoepassing.
* SKU-serie, bepaalt Hallo facturering. U kunt opgeven *Metereddata* voor een plan datalimiet en *Unlimiteddata* voor een onbeperkte gegevens-plan. U kunt facturering type Hallo van wijzigen *Metereddata* te*Unlimiteddata*, maar niet Hallo type uit *Unlimiteddata* te*Metereddata* .

> [!IMPORTANT]
> Uw ExpressRoute-circuit worden gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend. Zorg ervoor dat u deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.
> 
> 

Hallo-antwoord bevat de servicesleutel Hallo. U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende opdracht Hallo:

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Lijst van alle ExpressRoute-circuits
een lijst met alle Hallo ExpressRoute-circuits die u hebt gemaakt, tooget uitvoeren Hallo **Get-AzureRmExpressRouteCircuit** opdracht:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo `Get-AzureRmExpressRouteCircuit` cmdlet. Hallo aanroepen zonder parameters maken een lijst met alle Hallo-circuits. De sleutel van uw service wordt weergegeven in Hallo *ServiceKey* veld:

```powershell
Get-AzureRmExpressRouteCircuit
```


Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende opdracht Hallo:

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden
*ServiceProviderProvisioningState* bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde. Status biedt Hallo status op Hallo Microsoft aan clientzijde. Zie voor meer informatie over het circuit inrichtingstatuswaarden hello [werkstromen](expressroute-workflows.md#expressroute-circuit-provisioning-states) artikel.

Bij het maken van nieuwe ExpressRoute-circuit liggen Hallo circuit Hallo status te volgen:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



Hallo circuit verandert toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Voor u toobe kunnen toouse een ExpressRoute-circuit, moet het Hallo status volgende zijn:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren
Controle op Hallo status en status van Hallo circuit sleutel hello, laat u weten wanneer uw provider uw circuit is ingeschakeld. Nadat het Hallo-circuit is geconfigureerd, *ServiceProviderProvisioningState* wordt weergegeven als *ingericht*, zoals weergegeven in het volgende voorbeeld Hallo:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:

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

### <a name="7-create-your-routing-configuration"></a>7. Maken van uw configuratie van de routering
Zie voor stapsgewijze instructies Hallo [ExpressRoute-circuit routeringsconfiguratie](expressroute-howto-routing-arm.md) toocreate artikel en circuit peerings wijzigen.

> [!IMPORTANT]
> Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden. Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Koppelen van een virtueel netwerk tooan ExpressRoute-circuit
Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit. Gebruik Hallo [tooExpressRoute circuits koppelt virtuele netwerken](expressroute-howto-linkvnet-arm.md) artikel als u met Hallo Resource Manager-implementatiemodel werkt.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Hallo-status van een ExpressRoute-circuit ophalen
U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo **Get-AzureRmExpressRouteCircuit** cmdlet. Hallo aanroepen zonder parameters maken een lijst met alle Hallo-circuits.

```powershell
Get-AzureRmExpressRouteCircuit
```


antwoord Hallo zijn vergelijkbaar toohello voorbeeld te volgen:

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


U kunt informatie over een specifieke ExpressRoute-circuit krijgen door Hallo Resourcegroepnaam en de naam van het circuit wordt doorgegeven als een aanroep van de parameter toohello:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:

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


U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende opdracht Hallo:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Wijzigen van een ExpressRoute-circuit
U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.

U kunt doen Hallo zonder uitvaltijd te volgen:

* In- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.
* Hallo-bandbreedte verhoging van uw ExpressRoute-circuit mits capaciteit beschikbaar op Hallo-poort. Hallo bandbreedte van een circuit downgraden wordt niet ondersteund. 
* Hallo softwarelicentiecontrole plan van gegevens Datalimiet tooUnlimited gegevens wijzigen. Het wijzigen van Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.
* U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.

Raadpleeg voor meer informatie over limieten en beperkingen toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium-invoegtoepassing
U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit inschakelen met behulp van de volgende PowerShell-codefragment Hallo:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

Hallo circuit hebt nu Hallo ExpressRoute premium-invoegtoepassing voor functies die worden ingeschakeld. We begint facturering voor Hallo premium-invoegtoepassing mogelijkheid zodra Hallo-opdracht met succes is uitgevoerd.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium-invoegtoepassing
> [!IMPORTANT]
> Deze bewerking kan mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.
> 
> 

Let op Hallo volgende:

* Voordat u van premium toostandard downgraden, moet u ervoor zorgen dat virtuele netwerken die zijn gekoppeld, aantal Hallo toohello circuit is minder dan 10. Als u dit doet, uw aanvraag bijwerken mislukt en er worden kosten in rekening brengen volgens de premietarieven voor.
* U moet alle virtuele netwerken in andere geopolitieke regio's ontkoppelen. Als u dit doet, uw aanvraag bijwerken mislukt en er worden kosten in rekening brengen volgens de premietarieven voor.
* De routetabel moet minder dan 4000 routes voor persoonlijke peering. Uw tabel route is groter dan 4000 routes, Hallo BGP-sessie wordt neergezet als totdat Hallo aantal geadverteerde voorvoegsels daaronder 4.000 won't worden ingeschakeld.

U kunt Hallo-invoegtoepassing voor ExpressRoute premium voor een bestaand circuit Hallo uitschakelen met behulp van de volgende PowerShell-cmdlet Hallo:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>bandbreedte tooupdate hello ExpressRoute-circuit
Controleer voor ondersteunde bandbreedte-opties voor uw provider Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md). U kunt de grootte die groter zijn dan de grootte van uw bestaande circuit Hallo verzamelen.

> [!IMPORTANT]
> Mogelijk hebt u toorecreate hello ExpressRoute-circuit als er onvoldoende capaciteit op de bestaande poort Hallo. U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.
>
> U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren. Downgraden bandbreedte, moet u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.
> 

Nadat u welke grootte die u nodig hebt besluiten, uw circuit Hallo opdracht tooresize volgende gebruiken:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


Uw circuit, wordt in de Microsoft-zijde Hallo worden aangepast. U moet contact opnemen uw connectiviteit provider tooupdate-configuraties van hun kant toomatch deze wijziging. Nadat u deze melding, beginnen wij u facturering voor Hallo bijgewerkt bandbreedte optie.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>toomove hello SKU van gecontroleerde toounlimited
U kunt Hallo SKU van een ExpressRoute-circuit wijzigen met behulp van de volgende PowerShell-codefragment Hallo:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol toegang toohello klassieke en Resource Manager-omgevingen
Lees de instructies Hallo in [verplaatsen ExpressRoute-circuits vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Opheffen van inrichting en een ExpressRoute-circuit verwijderen
Let op Hallo volgende:

* U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit ontkoppelen. Als deze bewerking is mislukt, controleert u toosee als er geen virtuele netwerken zijn gekoppeld toohello circuit.
* Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht** moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant. We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.
* Als serviceprovider Hallo heeft gemaakt Hallo circuit (Hallo serviceprovider Inrichtingsstatus te is ingesteld**niet ingericht**) kunt u Hallo circuit verwijderen. Hiermee stopt u facturering voor Hallo circuit

U kunt uw ExpressRoute-circuit verwijderen door het uitvoeren van de volgende opdracht Hallo:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Volgende stappen

Nadat u het circuit hebt gemaakt, moet u Hallo te volgen:

* [Maken en aanpassen van routering voor ExpressRoute-circuit](expressroute-howto-routing-arm.md)
* [Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md)
