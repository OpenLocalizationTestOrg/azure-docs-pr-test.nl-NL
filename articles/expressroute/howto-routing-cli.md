---
title: 'Hoe tooconfigure routering voor een Azure ExpressRoute-circuit: CLI | Microsoft Docs'
description: In dit artikel helpt u bij het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Maken en aanpassen van routering voor een ExpressRoute-circuit met CLI

In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel met CLI. U kunt ook controleren Hallo status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit. Als u wilt dat een andere methode toowork toouse met uw circuit, selecteert u een artikel in Hallo volgende lijst:

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

* Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger) voordat u begint. Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).
* Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstroom](expressroute-workflows.md) voordat u begint met de configuratie-pagina's.
* U moet een actief ExpressRoute-circuit hebben. Hallo-instructies te volgen[maken van een ExpressRoute-circuit](howto-circuit-cli.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo opdrachten in dit artikel.

Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden. Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.

U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren. U kunt peerings configureren in elke gewenste volgorde. Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien.

## <a name="azure-private-peering"></a>Persoonlijke Azure-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit.

### <a name="toocreate-azure-private-peering"></a>toocreate persoonlijke Azure-peering

1. Hallo meest recente versie van Azure CLI installeren. Moet u de meest recente versie Hallo van hello Azure-opdrachtregelinterface (CLI). * revisie Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.

  ```azurecli
  az login
  ```

  Hallo-abonnement u wilt dat de ExpressRoute-circuit toocreate selecteren

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Maak een ExpressRoute-circuit. Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](howto-circuit-cli.md) en laat het inrichten door de connectiviteitsprovider Hallo.

  Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.
3. Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld. Gebruik Hallo voorbeeld te volgen:

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configureer persoonlijke Azure-peering voor Hallo circuit. Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:

  * Een/30 subnet voor de primaire koppeling Hallo. Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.
  * Een/30 subnet voor de secundaire koppeling Hallo. Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken. U kunt een persoonlijk AS-nummer voor deze peering gebruiken. Zorg dat u niet 65515 gebruikt.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.

  Gebruik Hallo voorbeeld tooconfigure Azure persoonlijke peering voor uw circuit te volgen:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure persoonlijke peering details

U kunt configuratie-informatie krijgen met behulp van Hallo voorbeeld te volgen:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure configuratie van persoonlijke peering

U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken. In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 100 too500 bijgewerkt.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete persoonlijke Azure-peering

U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:

> [!WARNING]
> U moet ervoor zorgen dat alle virtuele netwerken losgekoppeld van Hallo ExpressRoute-circuit zijn voordat u dit voorbeeld. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Openbare Azure-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.

### <a name="toocreate-azure-public-peering"></a>toocreate openbare Azure-peering

1. Hallo meest recente versie van Azure CLI installeren. Moet u de meest recente versie Hallo van hello Azure-opdrachtregelinterface (CLI). * revisie Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.

  ```azurecli
  az login
  ```

  Hallo-abonnement waarvoor u toocreate ExpressRoute-circuit wilt selecteren.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Maak een ExpressRoute-circuit.  Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](howto-circuit-cli.md) en laat het inrichten door de connectiviteitsprovider Hallo.

  Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u aanvragen dat uw connectiviteitsprovider mogelijk persoonlijke Azure-peering voor u maakt. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.
3. Controleer Hallo ExpressRoute-circuit tooensure is ingericht en ook ingeschakeld. Gebruik Hallo voorbeeld te volgen:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configureer openbare Azure-peering voor Hallo circuit. Zorg ervoor dat u de volgende informatie voordat u verder Hallo hebt.

  * Een/30 subnet voor de primaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
  * Een/30 subnet voor de secundaire koppeling Hallo. Dit moet een geldig openbaar IPv4-voorvoegsel zijn.
  * Een geldige VLAN-ID tooestablish deze peering. Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.
  * AS-nummer voor peering. U kunt 2-bytes en 4-bytes AS-nummers gebruiken.
  * **Optionele -** een MD5-hash, als u ervoor toouse een kiest.

  Voer Hallo voorbeeld tooconfigure Azure openbare peering voor uw circuit te volgen:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.

### <a name="tooview-azure-public-peering-details"></a>tooview Azure openbare peering details

U kunt krijgen configuratiegegevens wilt weergeven Hallo voorbeeld te volgen:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>configuratie van openbare peering Azure tooupdate

U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken. In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 200 too600 bijgewerkt.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete openbare Azure-peering

U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Microsoft-peering

Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit.

> [!IMPORTANT]
> Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Hallo Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd. Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit. Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft-peering

1. Hallo meest recente versie van Azure CLI installeren. Gebruik Hallo meest recente versie van Azure-opdrachtregelinterface (CLI) Hallo. * revisie Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.

  ```azurecli
  az login
  ```

  Hallo-abonnement waarvoor u toocreate ExpressRoute-circuit wilt selecteren.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Maak een ExpressRoute-circuit. Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](howto-circuit-cli.md) en laat het inrichten door de connectiviteitsprovider Hallo.

  Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen. In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo. Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.

3. Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld. Gebruik Hallo voorbeeld te volgen:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
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

   Voer Hallo voorbeeld tooconfigure Microsoft-peering voor uw circuit te volgen:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>details van tooget Microsoft-peering

U kunt configuratie-informatie krijgen met behulp van Hallo voorbeeld te volgen:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configuratie van tooupdate Microsoft-peering

U kunt elk deel van Hallo configuratie bijwerken. Hallo geadverteerde voorvoegsels van Hallo circuit vanuit 123.1.0.0/24 too124.1.0.0/24 in het volgende voorbeeld Hallo worden bijgewerkt:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft-peering

U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Volgende stappen

Volgende stap, [koppelen van een VNet tooan ExpressRoute-circuit](howto-linkvnet-cli.md).

* Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).
* Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).
* Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.