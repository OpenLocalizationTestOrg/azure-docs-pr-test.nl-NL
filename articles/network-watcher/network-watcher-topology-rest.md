---
title: aaaView Azure-netwerk-Watcher-topologie - REST-API | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse REST-API tooquery topologie van uw netwerk.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Netwerk-Watcher-topologie met REST-API weergeven

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

Hallo-topologie-functie van netwerk-Watcher biedt een visuele representatie van Hallo netwerkbronnen in een abonnement. In de portal Hallo is deze visualisatie opgenomen tooyou automatisch. Hallo gegevens achter Hallo Topologieweergave in de portal Hallo kan worden opgehaald via PowerShell.
Hierdoor kunt u meer mogelijkheden zoals Hallo gegevens kunnen worden gebruikt door andere hulpprogramma's voor toobuild uit Hallo visualisatie Hallo topologische informatie.

Hallo-koppeling is gemodelleerd onder twee-relaties.

- **Containment** -voorbeeld: VNet bevat een Subnet bevat een NIC
- **Gekoppeld** -voorbeeld: NIC is gekoppeld aan een virtuele machine

Hallo bevat volgende lijst eigenschappen die worden geretourneerd bij het opvragen van Hallo topologie REST-API.

* **naam** - hello naam van het Hallo-resource
* **id** -uri van de resource Hallo Hallo.
* **locatie** -Hallo locatie waar Hallo resource is opgeslagen.
* **koppelingen** -een lijst met koppelingen toohello verwijst naar object.
    * **naam** -naam Hallo Hallo waarnaar wordt verwezen resource.
    * **resourceId** -Hallo resourceId Hallo-uri van Hallo resource waarnaar wordt verwezen in Hallo-koppeling is.
    * **associationType** -Hallo relatie tussen Hallo onderliggend object en de bovenliggende Hallo wordt verwezen naar deze waarde. Geldige waarden zijn **bevat** of **gekoppelde**.

## <a name="before-you-begin"></a>Voordat u begint

In dit scenario moet u Hallo topologische informatie ophalen. ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell. ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel wordt antwoord van de Hallo-topologie voor een opgegeven resourcegroep opgehaald.

## <a name="log-in-with-armclient"></a>Meld u aan met ARMClient

Meld u bij tooarmclient met uw Azure-referenties.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Topologie ophalen

Hallo volgende voorbeeldtopologie aanvragen Hallo uit Hallo REST-API.  Hallo-voorbeeld is geparameteriseerd tooallow voor flexibiliteit bij het maken van een voorbeeld.  Vervang alle waarden met \< \> omsluiten.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

Hallo na antwoord is een voorbeeld van een kortere reactie die wordt geretourneerd wanneer de topologie voor een resourcegroup ophalen:

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

