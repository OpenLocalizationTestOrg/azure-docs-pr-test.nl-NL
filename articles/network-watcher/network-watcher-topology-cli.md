---
title: aaaView Azure-netwerk-Watcher-topologie - Azure CLI | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse Azure CLI tooquery topologie van uw netwerk.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a>Netwerk-Watcher-topologie met Azure CLI weergeven

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

Hallo-topologie-functie van netwerk-Watcher biedt een visuele representatie van Hallo netwerkbronnen in een abonnement. In de portal Hallo is deze visualisatie opgenomen tooyou automatisch. Hallo gegevens achter Hallo Topologieweergave in de portal Hallo kan worden opgehaald via PowerShell.
Hierdoor kunt u meer mogelijkheden zoals Hallo gegevens kunnen worden gebruikt door andere hulpprogramma's voor toobuild uit Hallo visualisatie Hallo topologische informatie.

Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux. Netwerk-Watcher gebruikt momenteel de Azure CLI 1.0 voor CLI-ondersteuning.

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

In dit scenario gebruikt u Hallo `network watcher topology` cmdlet tooretrieve Hallo topologische informatie. Er is ook een artikel over het te[ophalen netwerktopologie met REST-API](network-watcher-topology-rest.md).

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel wordt antwoord van de Hallo-topologie voor een opgegeven resourcegroep opgehaald.

## <a name="retrieve-topology"></a>Topologie ophalen

Hallo `network watcher topology` cmdlet haalt Hallo-topologie voor een opgegeven resourcegroep. Voeg Hallo argument '--json ' tooview hello oput in json-indeling

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Resultaten

Hallo resultaten hebben een eigenschap name 'Resources', waarin Hallo json antwoordtekst voor Hallo `network watcher topology` cmdlet.  Hallo-antwoord bevat Hallo bronnen Hallo Netwerkbeveiligingsgroep en de bijbehorende koppelingen (dat wil zeggen, bevat, gekoppelde).

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over Hallo beveiligingsregels voor verbindingen die toegepast tooyour netwerkbronnen in via zijn [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)
