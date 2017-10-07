---
title: Volgende Hop met Azure-netwerk-Watcher volgende Hop - REST aaaFind | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt zoeken welke Hallo type voor het volgende hop is en het IP-adres met behulp van volgende Hop hello Azure REST-API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met Azure REST API netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST-API](network-watcher-check-next-hop-rest.md)

De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen. Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.

## <a name="before-you-begin"></a>Voordat u begint

ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell. ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar het volgende hoptype hello en IP-adres voor een resource. toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).

U wordt in dit scenario:

* De volgende hop Hallo voor een virtuele machine worden opgehaald.

## <a name="log-in-with-armclient"></a>Meld u aan met ARMClient

Meld u bij tooarmclient met uw Azure-referenties.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Een virtuele machine ophalen

Hallo script tooreturn na een virtuele machine uitvoeren. Deze informatie is nodig voor het uitvoeren van volgende hop.

Hallo na code moet waarden voor Hallo variabelen te volgen:

- **subscriptionId** -Hallo toouse voor abonnement-Id.
- **resourceGroupName** - hello naam van een resourcegroep die virtuele machines bevatten.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Hallo-id van Hallo virtuele machine wordt van de volgende Hallo uitvoer, gebruikt in Hallo voorbeeld te volgen:

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Ophalen van de volgende Hop

Zodra Hallo autorisatie-header is gemaakt, kan de volgende hop Hallo van een virtuele machine worden opgehaald. Hallo moeten volgende waarden worden vervangen voor Hallo code voorbeeld toowork.

> [!Important]
> Voor de REST-API voor netwerk-Watcher Hallo aanroepen Resourcegroepnaam in Hallo aanvraag-URI is Hallo-resourcegroep met Hallo netwerk-Watcher niet Hallo-bronnen zoals u Hallo diagnostische acties uitvoert op.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Volgende hop is vereist dat de VM-resource Hallo toorun wordt toegewezen.

## <a name="results"></a>Resultaten

Hallo bevat volgende fragment een voorbeeld van uitvoer van Hallo ontvangen. Hallo resultaten bevatten Hallo volgende waarden:

* **nextHopType** -deze waarde is een van de volgende waarden Hallo: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway of None.
* **nextHopIpAddress** -IP-adres van de volgende hop Hallo Hallo.
* **routeTableId** - Hallo-waarde is ofwel een uri voor de routetabel Hallo Hallo route gekoppeld of als geen gebruiker gedefinieerde route is gedefinieerd Hallo-waarde van *Systeemroute* wordt geretourneerd.

Hallo volgen Hallo resulteert in een json-indeling.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Volgende stappen

Als u kunnen toofind uit de volgende hop Hallo voor een virtuele machine zijn, kunt u Hallo beveiliging van uw netwerkresources bekijken in via [overzicht van de beveiliging](network-watcher-security-group-view-overview.md)














