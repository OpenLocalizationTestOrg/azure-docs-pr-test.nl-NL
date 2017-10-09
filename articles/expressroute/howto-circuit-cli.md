---
title: 'Maken en wijzigen van een Azure ExpressRoute-circuit: CLI | Microsoft Docs'
description: Dit artikel wordt beschreven hoe toocreate, inrichten, controleren, bijwerken, verwijderen en een ExpressRoute-circuit met CLI inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Maken en een ExpressRoute-circuit met CLI wijzigen


Dit artikel wordt beschreven hoe een Azure ExpressRoute-circuit met behulp van toocreate Hallo opdrachtregelinterface (CLI). Dit artikel ziet u ook hoe toocheck Hallo status, bijwerken, of verwijderen en een circuit inrichting ervan ongedaan maakt. Als u een andere methode toowork met ExpressRoute-circuits toouse wilt, kunt u Hallo artikel van Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure-CLI](howto-circuit-cli.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klassiek)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Voordat u begint

* Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger) voordat u begint. Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli) en [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).
* Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.

## <a name="create-and-provision-an-expressroute-circuit"></a>Maken en een ExpressRoute-circuit inrichten

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Meld u aan tooyour Azure-account en uw abonnement te selecteren

toobegin uw configuratie, aanmelden tooyour Azure-account. Gebruik Hallo volgen voorbeelden toohelp die u verbinding kunt maken:

```azurecli
az login
```

Controleer de abonnementen Hallo voor Hallo-account.

```azurecli
az account list
```

Hallo-abonnement waarvoor u een ExpressRoute-circuit toocreate wilt selecteren.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Hallo-lijst met ondersteunde providers, locaties en bandbreedten

Voordat u een ExpressRoute-circuit maken, moet u Hallo lijst met ondersteunde connectiviteitsproviders, locaties en bandbreedte-opties. CLI-opdracht 'az netwerk express route lijst-service-providers' Hello retourneert deze informatie, die u in latere stappen:

```azurecli
az network express-route list-service-providers
```

Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Controleer Hallo antwoord toosee als uw connectiviteitsprovider wordt weergegeven. Maak een notitie van Hallo informatie die u bij het maken van een circuit dient te volgen:

* Naam
* PeeringLocations
* BandwidthsOffered

U bent nu klaar toocreate een ExpressRoute-circuit.

### <a name="3-create-an-expressroute-circuit"></a>3. Een ExpressRoute-circuit maken

> [!IMPORTANT]
> Uw ExpressRoute-circuit wordt gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend. Deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.
> 
> 

Als u nog een resourcegroep hebt, moet u een maken voordat u uw ExpressRoute-circuit maken. U kunt een resourcegroep maken door het uitvoeren van de volgende opdracht Hallo:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

Hallo volgende voorbeeld ziet u hoe toocreate een 200 Mbps-ExpressRoute-circuit via Equinix in Silicon Valley. Als u een andere provider en andere instellingen gebruikt, vervangt u die informatie door wanneer u uw aanvraag. 

Zorg ervoor dat u de juiste SKU-laag Hallo en SKU-serie opgeeft:

* SKU-laag bepaalt of een standaard ExpressRoute of een premium-invoegtoepassing voor ExpressRoute is ingeschakeld. U kunt 'Standaard' tooget Hallo standaard SKU- of Premium voor Hallo premium-invoegtoepassing opgeven.
* SKU-serie, bepaalt Hallo facturering. U kunt 'Metereddata' voor een datalimiet plannings- en 'Unlimiteddata' opgeven voor een onbeperkte gegevens-plan. U kunt facturering type van het 'Metereddata 'too'Unlimiteddata', maar type niet wijzigen Hallo van 'Unlimiteddata' too'Metereddata' Hallo wijzigen.


Uw ExpressRoute-circuit wordt gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend. Hallo volgende voorbeeld wordt een aanvraag voor een nieuwe servicesleutel:

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

Hallo-antwoord bevat de servicesleutel Hallo.

### <a name="4-list-all-expressroute-circuits"></a>4. Lijst van alle ExpressRoute-circuits

een lijst met alle Hallo ExpressRoute-circuits die u hebt gemaakt, tooget Hallo 'az express route lijst met netwerken' opdracht uitvoeren. Met deze opdracht kunt u deze informatie op elk gewenst moment ophalen. toolist alle circuits zorg Hallo aanroepen zonder parameters.

```azurecli
az network express-route list
```

De sleutel van uw service wordt vermeld in Hallo *ServiceKey* antwoord Hallo veld.

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

U kunt gedetailleerde beschrijvingen van alle Hallo parameters ophalen door actieve Hallo-opdracht met Hallo '-h' parameter.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden

'ServiceProviderProvisioningState' bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde. Hallo status biedt Hallo status op Hallo Microsoft aan clientzijde. Zie voor meer informatie, Hallo [werkstromen artikel](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Bij het maken van nieuwe ExpressRoute-circuit heeft Hallo circuit Hallo status te volgen:

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

Hallo circuit wijzigingen toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Voor u toobe kunnen toouse een ExpressRoute-circuit, moet het Hallo status volgende zijn:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren

Controle op Hallo status en status van Hallo circuit sleutel hello, laat u weten wanneer uw provider uw circuit is ingeschakeld. Nadat het Hallo-circuit is geconfigureerd, is 'ServiceProviderProvisioningState' wordt weergegeven als 'Ingericht', zoals wordt weergegeven in het volgende voorbeeld Hallo:

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Maken van uw configuratie van de routering

Zie voor stapsgewijze instructies Hallo [ExpressRoute-circuit routeringsconfiguratie](howto-routing-cli.md) toocreate artikel en circuit peerings wijzigen.

> [!IMPORTANT]
> Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden. Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureert en beheert routering voor u.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Koppelen van een virtueel netwerk tooan ExpressRoute-circuit

Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit. Gebruik Hallo [tooExpressRoute circuits koppelt virtuele netwerken](howto-linkvnet-cli.md) artikel.

## <a name="modify"></a>Wijzigen van een ExpressRoute-circuit

U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit. Kunt u de volgende wijzigingen zonder uitvaltijd Hallo maken:

* U kunt in- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.
* U kunt de bandbreedte Hallo van uw ExpressRoute-circuit vergroten mits er capaciteit beschikbaar is op Hallo-poort. Echter, Hallo bandbreedte van een circuit downgraden wordt niet ondersteund. 
* U kunt Hallo softwarelicentiecontrole plan wijzigen van gegevens Datalimiet tooUnlimited gegevens. Het wijzigen van echter Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.
* U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.

Zie voor meer informatie over limieten en beperkingen Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium-invoegtoepassing

U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit inschakelen met behulp van de volgende opdracht Hallo:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

Hallo-circuit heeft nu Hallo ExpressRoute premium-invoegtoepassing voor functies die worden ingeschakeld. We beginnen facturering voor Hallo premium-invoegtoepassing mogelijkheid zodra Hallo-opdracht met succes is uitgevoerd.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium-invoegtoepassing

> [!IMPORTANT]
> Deze bewerking kan mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.
> 
> 

Begrijpen voordat Hallo ExpressRoute premium-invoegtoepassing is uitgeschakeld, Hallo volgende criteria:

* Voordat u van premium toostandard downgraden, moet u ervoor zorgen dat er minder dan 10 virtuele netwerken gekoppelde toohello circuit. Als u meer dan 10 hebt, uw aanvraag bijwerken mislukt en er kosten in rekening brengen volgens de premietarieven voor.
* U moet alle virtuele netwerken in andere geopolitieke regio's ontkoppelen. Als u niet alle virtuele netwerken ontkoppelt, mislukt de updateaanvraag en we u volgens de premietarieven voor rekening.
* De routetabel moet minder dan 4000 routes voor persoonlijke peering. Als uw tabel route groter dan 4000 routes is, zakt Hallo BGP-sessie. Hallo sessie won't totdat het aantal geadverteerde voorvoegsels Hallo lager dan 4000 is worden ingeschakeld.

U kunt Hallo-invoegtoepassing voor ExpressRoute premium voor een bestaand circuit Hallo uitschakelen met behulp van Hallo voorbeeld te volgen:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>bandbreedte tooupdate hello ExpressRoute-circuit

Controleer voor Hallo ondersteund bandbreedte-opties voor uw provider, Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md). U kunt de grootte die groter zijn dan de grootte van uw bestaande circuit Hallo verzamelen.

> [!IMPORTANT]
> Als er onvoldoende capaciteit op de bestaande poort hello, mogelijk hebt u toorecreate hello ExpressRoute-circuit. U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.
>
> U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren. Bandbreedte downgraden vereist u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.
>

Nadat u hebt besloten Hallo grootte die u nodig hebt, uw circuit Hallo opdracht tooresize volgende gebruiken:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

Uw circuit wordt aangepast Hallo Microsoft zijde. Vervolgens maakt u moet contact opnemen met uw connectiviteit provider tooupdate-configuraties van hun kant toomatch deze wijziging. Nadat u deze melding, beginnen wij u facturering voor Hallo bijgewerkt bandbreedte optie.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>toomove hello SKU van gecontroleerde toounlimited

U kunt Hallo SKU van een ExpressRoute-circuit wijzigen met behulp van Hallo voorbeeld te volgen:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol toegang toohello klassieke en Resource Manager-omgevingen

Lees de instructies Hallo in [verplaatsen ExpressRoute-circuits vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Opheffen van inrichting en een ExpressRoute-circuit verwijderen

toodeprovision en een ExpressRoute-circuit verwijderen Zorg er dan voor dat u begrijpt Hallo volgende criteria:

* U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit ontkoppelen. Als deze bewerking is mislukt, controleert u toosee als er geen virtuele netwerken zijn gekoppeld toohello circuit.
* Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht**, moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant. We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.
* U kunt Hallo circuit verwijderen als serviceprovider Hallo heeft gemaakt Hallo circuit. Wanneer een circuit is gemaakt, Hallo serviceprovider Inrichtingsstatus te ingesteld**niet ingericht**. Hierdoor wordt voorkomen dat facturering voor Hallo circuit.

U kunt uw ExpressRoute-circuit verwijderen door het uitvoeren van de volgende opdracht Hallo:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

Nadat u het circuit hebt gemaakt, zorg dat u Hallo volgende taken:

* [Maken en aanpassen van routering voor ExpressRoute-circuit](howto-routing-cli.md)
* [Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit](howto-linkvnet-cli.md)
